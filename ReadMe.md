# GlideUtils
Glide图片加载库的封装类
占位符 不会覆盖CircleImageView，支持直接加载静态图、动态图到View，或者获取Bitmap，Drawable。加载普通图片可以加参数设置占位符和错误图

普通加载图片(支持CircleImageView)：
```

GlideUtils.loadImage(url, imageview);

//GlideUtils.loadImage(this, url, imageview, null);



```
需要添加占位图和错误图在后面加：
```
GlideUtils.loadImage(this, url, imageview, null, R.drawable.default_article_image, R.drawable.default_article_image);

```

加载Gif图片，带监听

```Java
GlideUtils.loadImageGif(mImageUrl, mImageView, new GlideUtils.ImageLoadListener<String, GifDrawable>() {
                @Override
                public void onLoadingComplete(String uri, ImageView view, GifDrawable resource) {
                    progressBar.setVisibility(View.GONE);

                }

                @Override
                public void onLoadingError(String source, Exception e) {
                    LogUtil.e("im查看图片加载失败:"+e);
                    mEntry.setIsDownload(false);
                    progressBar.setVisibility(View.GONE);
                    mFailLayout.setVisibility(View.VISIBLE);
                }
            });
```
不带监听就设置把监听属性设置我为null;


加载静态图片
```Java
GlideUtils.loadImage(this, mImageUrl, mImageView, new GlideUtils.ImageLoadListener<String, GlideDrawable>() {
                        @Override
                        public void onLoadingComplete(String uri, ImageView view, GlideDrawable resource) {
                            progressBar.setVisibility(View.GONE);
                            mEntry.setIsDownload(true);
                        }

                        @Override
                        public void onLoadingError(String source, Exception e) {
                            LogUtil.e("im查看图片加载失败:" +e + "连接:" + source);
                            mEntry.setIsDownload(false);
                            progressBar.setVisibility(View.GONE);
                            mFailLayout.setVisibility(View.VISIBLE);
                        }
                    });
```


**重要一点**，在多图片的界面destory之后，在onDestory回调方法调用
```Java
   @Override
    protected void onDestroy() {
        super.onDestroy();
        GlideUtils.clearMemory(this);
        System.gc();
    }

```



其他等等



