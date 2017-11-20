# chameleon
Mini Face-recognition Client 简单的人脸识别端小脚本

## 环境要求
*  Python-3.4+
*  PostgreSQL-9.6.3
*  OpenCV3
*  dlib-19.4
*  docker-17.06（推荐）

## 起步

+ **环境搭建**

可以参考洋吴克的[教程](https://www.pyimagesearch.com/2017/04/17/real-time-facial-landmark-detection-opencv-python-dlib/)。

当然如果你嫌烦，或者机器真的有问题怎么也装不成功，那可以尝试我们自制的[docker镜像](https://hub.docker.com/r/adoo/python3-opencv3-dlib/)，tag为`mana`。

+ **运行**

如果你是直接用的本机环境，直接运行`singledetector.py`就可以了,eg:

``` shell
> python3 singledetector.py -r rtsp://admin:admin123@192.168.2.95:554/h264/ch01/main/av_stream -s 0.8 
```

如果用docker，请运行

``` shell
> docker run -dit -v /your/code/path:/srv/chameleon --name face adoo/python3-opencv3-dlib 
```

+ **视频源**

默认是调用本机的摄像头，用`-r`参数控制。同时也接受所有满足rtsp协议的视频源。详见[singledetector.py line15](https://github.com/MagicAcademy/chameleon/blob/master/singledetector.py#L15) 的注释说明。

+ **原理介绍**

[用深度学习识别人脸](https://zhuanlan.zhihu.com/p/24567586)

此脚本也是用的欧式测距，128个特征值作为矩阵存放在了postgresql中（也可以换成nosql数据库）。

+ **导入数据**

可以利用 `init_faces.py` 导入你需要的人脸数据，源数据可以是满满一文件夹的头像。

图片名就是这张脸的唯一名字。

## 一些错误解决方案
- [dyld: Library not loaded: /usr/local/lib/libjpeg.8.dylib - homebrew php](https://stackoverflow.com/questions/32703296/dyld-library-not-loaded-usr-local-lib-libjpeg-8-dylib-homebrew-php)
