# GlideUtils
Glide图片加载库的封装类
占位符 不会覆盖CircleImageView，支持直接加载静态图、动态图到View，或者获取Bitmap，Drawable。加载普通图片可以加参数设置占位符和错误图

加载Gif图片，带监听

```Java
GlideUtils.loadImageGif(mImageUrl, mImageView, new GlideUtils.ImageLoadListener() {

                @Override
                public <T, K> void onLoadingComplete(T uri, ImageView view, K resource) {
                    progressBar.setVisibility(View.GONE);
                }

                @Override
                public <T> void onLoadingError(T source, String errorMsg) {
                    LogUtil.e("im查看图片加载失败:"+errorMsg);
                    mEntry.setIsDownload(false);
                    ToastUtil.showCustomToast(getActivity(), "图片加载失败!");
                    progressBar.setVisibility(View.GONE);
                    mFailLayout.setVisibility(View.VISIBLE);
                }
            });
```
不带监听就设置把监听属性设置我为null;


加载静态图片
```Java
GlideUtils.loadImage( mImageUrl, mImageView, new GlideUtils.ImageLoadListener() {

              @Override
                public <T, K> void onLoadingComplete(T uri, ImageView view, K resource) {
                    progressBar.setVisibility(View.GONE);
                    mEntry.setIsDownload(true);

                }

                @Override
                public <T> void onLoadingError(T source, String errorMsg) {
                    LogUtil.e("im查看图片加载失败:"+errorMsg+"\n连接:"+source);
                    mEntry.setIsDownload(false);
                    ToastUtil.showCustomToast(getActivity(), "图片加载失败!");
                    progressBar.setVisibility(View.GONE);
                    mFailLayout.setVisibility(View.VISIBLE);
                }
            });
```

获取Drawable
```Java
GlideUtils.loadImage(this, mImageUrl, new GlideUtils.ImageLoadListener() {
                @Override
                public <T, K> void onLoadingComplete(T uri, ImageView view, K resource) {
                    mImageView.setImageDrawable((GlideDrawable) resource);
                }

                @Override
                public <T> void onLoadingError(T source, String errorMsg) {
                    //加载失败处理
                }
            });
            
```

重要一点，在多图片的界面destory之后，在onDestory回调方法调用
```Java
   @Override
    protected void onDestroy() {
        super.onDestroy();
        GlideUtils.clearMemory(this);
        System.gc();
    }

```



其他等等



