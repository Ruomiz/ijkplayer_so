## 环境配置 ##
	
先放官网地址：[ijkplayer](https://github.com/Bilibili/ijkplayer)

此次编译是在ubuntu下编译的，需要下载VMware虚拟机和ubuntu系统。
编译ijkplayer时是需要SDK和NDK的（linux版本）,SDK和NDK环境需要在ubuntu上配置好。其实这些文件是可以在windows上下载好，然后复制到ubuntu上的，但不能直接复制，需要下载WinSCP和PuTTY（它的主要功能就是在本地与远程计算机间安全的复制文件）。

## 开始编译 ##
1.启动虚拟机，打开shell命令输入：
	
	
	sudo apt-get update
	sudo apt-get install git
	sudo apt-get install yasm

	//上面是命令是安装git和yasm

2：配置ndk和sdk

配置ndk和skd，只需要命令行输入：

	export ANDROID_NDK=<your ndk path>	
	export ANDROID_SDK=<your sdk path>
	
我在ubuntu下的ndk路径如下：

![](http://oo2ge5zz3.bkt.clouddn.com/ndk_build.png)

直接在shell中输入：

![](http://oo2ge5zz3.bkt.clouddn.com/export.png)

配置SDK方法和上面一样（linux版本）。

3.开始编译：

**如果要编译出来的ijkplayer支持https，则需要编译OpenSSL(https就是http的加密版，即http+加密协议，加密协议一般为ssl或者TSL，OpenSSL是一套开源工具集，实现了ssl和TSL协议**)
	
	//clone ijkplayer到本地
	git clone https://github.com/Bilibili/ijkplayer.git ijkplayer-android

	//切换到源码目录
	cd ijkplayer-android 	

	//检查版本
	git checkout -B latest k0.8.4

	//初始化
	./init-android.sh

	//下载OpenSSL
	./init-android-openssl.sh	

	//切换到android/contrib 目录下，编译脚本在这个目录下
	cd android/contrib

	// 编译 OpenSSL
	./compile-openssl.sh clean
	./compile-openssl.sh all

	//编译FFmpeg
	./compile-ffmpeg.sh clean
	./compile-ffmpeg.sh all

	//返回ijkplayer/android 目录，编译ijkplayer的so库
	cd ..
	./compile-ijk.sh all

## 编译完成 ##

按照上面命令依次执行,最后编译完成时如下图：
![](http://oo2ge5zz3.bkt.clouddn.com/ijk_over.png)


ijkplayer目录如下：
![](http://oo2ge5zz3.bkt.clouddn.com/ijk_dir.png)

**编译完成后可以在ijkplayer-android/android/ijkplayer中查看生成的对应so文件。可以直接用AndroidStudio打开。**

![](http://oo2ge5zz3.bkt.clouddn.com/so.png)


## 运行 ##
用AdnroidStudio打开该工程，编译运行

![](http://oo2ge5zz3.bkt.clouddn.com/asdir.png)

以上就已经是编译好的ijkPlayer工程。可以将so复制到一个自己独立的工程然后对ijkplayer进行对应的封装即可。
