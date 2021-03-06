## 坐标系统转


作者：康林(kl222@126.com)  
项目地址：https://github.com/KangLin/TransformCoordinate  

------------
[![Windows build status](https://ci.appveyor.com/api/projects/status/yxkcu6b6o2av6wmk?svg=true)](https://ci.appveyor.com/project/KangLin/transformcoordinate)  
[![Linux build Status](https://travis-ci.org/KangLin/TransformCoordinate.svg?branch=master)](https://travis-ci.org/KangLin/TransformCoordinate)

------------

### 介绍
本项目对WGS84、GCJ02、百度坐标系之间进行转换。

WGS84：为一种大地坐标系，也是目前广泛使用的GPS全球卫星定位系统使用的坐标系。  
GCJ02：又称火星坐标系，是由中国国家测绘局制定的地理坐标系统，是由WGS84加密后得到的坐标系。  
BD09：为百度坐标系，在GCJ02坐标系基础上再次加密。其中bd09ll表示百度经纬度坐标，bd09mc表示百度墨卡托米制坐标。  

本项目还包括一个GPX文件操作模块。

本项目包含：  
- 坐标转换库：TransformCoordinate  
- GPX文件操作库：GpxModel  
- 坐标转换程序：TransformCoordinateApp  

------------

### [下载安装包](https://github.com/KangLin/TransformCoordinate/releases/latest)

- linux
    - [TransformCoordinate_v0.0.9.tar.gz](https://github.com/KangLin/TransformCoordinate/releases/download/v0.0.9/TransformCoordinate_v0.0.9.tar.gz)  
      AppImage格式的执行程序，可直接运行在linux系统，详见：https://appimage.org/  
      使用:    
      1. 解压。复制TransformCoordinate_v0.0.9.tar.gz到安装目录，然后解压：

                mkdir TransformCoordinate
                cd TransformCoordinate
                cp $DOWNLOAD/TransformCoordinate_v0.0.9.tar.gz .
                tar xvfz TransformCoordinate_v0.0.9.tar.gz

      2. 安装
        
                ./install1.sh install TransformCoordinate
        
      3. 如果需要，卸载
        
                ./install1.sh remove TransformCoordinate

- ubuntu
    - [transformcoordinate_0.0.9_amd64.deb](https://github.com/KangLin/TransformCoordinate/releases/download/v0.0.9/transformcoordinate_0.0.9_amd64.deb)  
  deb 安装包,可用于　Ubuntu
  
- windows
    - [TransformCoordinate-Setup-v0.0.9.exe](https://github.com/KangLin/TransformCoordinate/releases/download/v0.0.9/TransformCoordinate-Setup-v0.0.9.exe)  
  Windows安装包，支持 Windows xp 以上系统 

- android
    + [TransformCoordinate_v0.0.9.apk](https://github.com/KangLin/TransformCoordinate/releases/download/v0.0.9/TransformCoordinate_v0.0.9.apk)

------------

## 编译
### 下载源码

    git clone https://github.com/KangLin/TransformCoordinate.git

### 依赖
+ 编译工具
  + [Qt](http://qt.io/)
  + 编译器
    - For linux or android
        + GNU Make 工具
        + GCC 或者 Clang 编译器
    - For windows
        + [MSVC](http://msdn.microsoft.com/zh-cn/vstudio)
        + MinGW
  + [CMake](http://www.cmake.org/)
+ 依赖库
  - [必选] Rabbit 公共库: https://github.com/KangLin/RabbitCommon
  
### CMake 配置参数
  - [必选] Qt5_DIR: qt 安装位置
  - [必选] RabbitCommon_DIR: RabbitCommon 源码位置

### 各平台编译
#### linux 平台编译说明
  - 编译

        cd TransformCoordinate
        mkdir build
        cd build
        cmake .. -DCMAKE_INSTALL_PREFIX=`pwd`/install \
                 -DCMAKE_BUILD_TYPE=Release \
                 -DQt5_DIR= \
                 -DRabbitCommon_DIR= \
                 [其它可选 CMake 配置参数]
        cmake --build . --config Release 

  - 安装

        cmake --build . --config Release --target install 

  - 运行例子
    + 把生成库的目录加入到变量 LD_LIBRARY_PATH 中
 
            export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:`pwd`/bin

    + 执行 bin 目录下的程序

            cd TransformCoordinate
            cd build
            cd bin
            ./TransformCoordinateApp

#### windows 平台编译说明
  - 使用 cmake-gui.exe 工具编译。打开 cmake-gui.exe 配置
  - 命令行编译
    + 把 cmake 命令所在目录加入到环境变量 PATH 中
    + 从开始菜单打开 “VS2015开发人员命令提示”，进入命令行

      - 编译

            cd TransformCoordinate
            mkdir build
            cd build
            cmake .. -DCMAKE_INSTALL_PREFIX=`pwd`/install \
                 -DCMAKE_BUILD_TYPE=Release \
                 -DQt5_DIR= \
                 -DRabbitCommon_DIR= \
                 [其它可选 CMake 配置参数]
            cmake --build . --config Release

      - 安装

            cmake --build . --config Release --target install

      - 运行例子
        + 执行 bin 目录下的程序
          - TransformCoordinateApp

#### Android 平台编译说明
+ 安装 ndk 编译工具
  - 从 https://developer.android.com/ndk/downloads 下载 ndk，并安装到：/home/android-ndk
  - 设置环境变量：

        export ANDROID_NDK=/home/android-ndk
        
+ 安装 sdk 工具
  - 从 https://developer.android.google.cn/studio/releases 下载 sdk tools, 并安装到 /home/android-sdk
  - 设置环境变量：
  
        export ANDROID_SDK=/home/android-sdk

+ 编译
  - 主机是 linux

        cd TransformCoordinate
        mkdir build
        cd build
        cmake .. -DCMAKE_INSTALL_PREFIX=`pwd`/android-build \
                 -DCMAKE_BUILD_TYPE=Release \
                 -DCMAKE_TOOLCHAIN_FILE=${ANDROID_NDK}/build/cmake/android.toolchain.cmake \
                 -DANDROID_ABI="armeabi-v7a with NEON" \
                 -DANDROID_PLATFORM=android-18 \
                 -DQt5_DIR= \
                 -DRabbitCommon_DIR= \
                 [其它可选 CMake 配置参数]
        cmake --build . --config Release --target install
        cmake --build . --config Release --target APK

  - 主机是 windows

        cd TransformCoordinate
        mkdir build
        cd build
        cmake .. -DCMAKE_INSTALL_PREFIX=`pwd`/android-build \
                 -G"Unix Makefiles" -DCMAKE_BUILD_TYPE=Release \
                 -DCMAKE_TOOLCHAIN_FILE=${ANDROID_NDK}/build/cmake/android.toolchain.cmake \
                 -DCMAKE_MAKE_PROGRAM=${ANDROID_NDK}/prebuilt/windows-x86_64/bin/make.exe \
                 -DANDROID_ABI=arm64-v8a \
                 -DANDROID_ARM_NEON=ON \
                 -DQt5_DIR= \
                 -DRabbitCommon_DIR= \
                 [其它可选 CMake 配置参数]
        cmake --build . --config Release --target install
        cmake --build . --config Release --target APK

  - CMake for android 参数说明：https://developer.android.google.cn/ndk/guides/cmake
    + ANDROID_ABI: 可取下列值：
      目标 ABI。如果未指定目标 ABI，则 CMake 默认使用 armeabi-v7a。  
      有效的目标名称为：
      - armeabi：带软件浮点运算并基于 ARMv5TE 的 CPU。
      - armeabi-v7a：带硬件 FPU 指令 (VFPv3_D16) 并基于 ARMv7 的设备。
      - armeabi-v7a with NEON：与 armeabi-v7a 相同，但启用 NEON 浮点指令。这相当于设置 -DANDROID_ABI=armeabi-v7a 和 -DANDROID_ARM_NEON=ON。
      - arm64-v8a：ARMv8 AArch64 指令集。
      - x86：IA-32 指令集。
      - x86_64 - 用于 x86-64 架构的指令集。
    + ANDROID_NDK <path> 主机上安装的 NDK 根目录的绝对路径
    + ANDROID_PLATFORM: 如需平台名称和对应 Android 系统映像的完整列表，请参阅 [Android NDK 原生 API](https://developer.android.google.cn/ndk/guides/stable_apis.html)
    + ANDROID_ARM_MODE
    + ANDROID_ARM_NEON
    + ANDROID_STL: 指定 CMake 应使用的 STL。默认情况下，CMake 使用 c++_static。 
      - c++_shared: 使用 libc++ 动态库
      - c++_static: 使用 libc++ 静态库
      - none: 没有 C++ 库支持
      - system: 用系统的 STL
  - 安装 apk 到设备

       adb install android-build-debug.apk 

------------

### 捐赠:  
本软件如果对你有用，或者你喜欢它，请你捐赠，支持作者。谢谢！

[![捐赠](https://gitee.com/kl222/RabbitCommon/raw/master/Src/Resource/image/Contribute.png "捐赠")](https://github.com/KangLin/RabbitCommon/raw/master/Src/Resource/image/Contribute.png "捐赠")

------------

### 参见：  
http://lbsyun.baidu.com/index.php?title=TransformCoordinate  
http://www.360doc.com/content/16/0721/16/9200790_577327509.shtml
