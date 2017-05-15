# Android 处理过大的图片
OOM  或者　Bitmap too large to be uploaded into a texture

## Bitmap too large to be uploaded into a texture
问题：硬件加速对图片的大小有限制。

一个办法：

	<application android:hardwareAccelerated="false" ...>
禁止硬件加速（这是所谓的简单粗暴的方法，我承认我无耻了）

比较好的解决方法是类似google map的实现：将图片分成不同的块，每次加载需要的块。android提供了[一个方法][1]： BitmapRegionDecoder.html

再一个办法：　Bitmap使用前进行压缩，　压小一点就能用了．


    public static Bitmap compress(Bitmap image, int maxW, int maxH) {

        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        image.compress(Bitmap.CompressFormat.JPEG, 100, baos);
        if (baos.toByteArray().length / 1024 > 1024) {// 判断如果图片大于1M
            // 压缩,进行压缩避免在生成图片（BitmapFactory.decodeStream）时溢出
            baos.reset();// 重置baos即清空baos
            image.compress(Bitmap.CompressFormat.JPEG, 50, baos);// 这里压缩50%，把压缩后的数据存放到baos中
        }
        ByteArrayInputStream isBm = new ByteArrayInputStream(baos.toByteArray());
        BitmapFactory.Options newOpts = new BitmapFactory.Options();
        // 开始读入图片，此时把options.inJustDecodeBounds 设回true了
        newOpts.inJustDecodeBounds = true;
        Bitmap bitmap = BitmapFactory.decodeStream(isBm, null, newOpts);
        newOpts.inJustDecodeBounds = false;
        int w = newOpts.outWidth;
        int h = newOpts.outHeight;

        // 缩放比。由于是固定比例缩放，只用高或者宽其中一个数据进行计算即可
        int be = 1;// be=1表示不缩放
        if (w > h && w > maxW) {// 如果宽度大的话根据宽度固定大小缩放
            be = (int) (newOpts.outWidth / maxW);
        } else if (w < h && h > maxH) {// 如果高度高的话根据宽度固定大小缩放
            be = (int) (newOpts.outHeight / maxH);
        }
        if (be <= 0)
            be = 1;
        newOpts.inSampleSize = be;// 设置缩放比例
        newOpts.inPreferredConfig = Bitmap.Config.RGB_565;// 降低图片从ARGB888到RGB565
        // 重新读入图片，注意此时已经把options.inJustDecodeBounds 设回false了
        isBm = new ByteArrayInputStream(baos.toByteArray());
        bitmap = BitmapFactory.decodeStream(isBm, null, newOpts);
        return bitmap;
    }



refs:  
[硬件加速官方文档](http://developer.android.com/guide/topics/graphics/hardware-accel.html)  

[Android处理图片OOM的若干方法小结 ](http://www.2cto.com/kf/201208/148379.html)  
[Android加载大图片OOM异常解决](http://www.cnblogs.com/jevan/archive/2012/07/05/2577942.html)  
[Android 图片加载Bitmap OOM错误解决办法](http://www.chengxuyuans.com/Android/67291.html)  
[android中加载图片时出现oom](http://www.kaifajie.cn/android/7645.html)  
[【Android】大图片加载时OOM](http://www.th7.cn/Program/Android/201310/153987.shtml)  
[解决：Bitmap too large to be uploaded into a texture exception ](http://blog.csdn.net/geekpark/article/details/8981145)  
[Android中的硬件加速](http://blog.csdn.net/geekpark/article/details/8981154)  




[1]: http://developer.android.com/reference/android/graphics/BitmapRegionDecoder.html
