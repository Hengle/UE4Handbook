# Use WebRTC In Unreal Engine 4

## WebRTC安卓编译
    只有一台Windows的电脑。三个方案，完成WebRTC的Android平台编译。

---
## 必要的准备
    一个良好的梯子！！！这点很重要！很重要！很重要！大多过程中的问题都源自于网络问题。
* 科学上网
    - blinkload  
        个人的推广链接: https://blinkload.to/aff/UXiq
    - clash for windows  
        github地址: https://github.com/Fndroid/clash_for_windows_pkg/releases

---
### 方案一：适用于Linux的Windows子系统（推荐）

* 启用子系统  
    -控制面板  
    -程序和功能  
    -启用或关闭Windows功能  
    -适用于Linux的Windows子系统  
* UWP版Ubuntu  
    -Microsoft Store  
    -Ubuntu
* Windows Terminal  
    -Microsoft Store  
    -Windows Terminal
* 创建工作目录  
    cd /mnt/  
    cd /e/（随便哪个盘，体验Windows与Liunx的合体，无缝访问）  
    mkdir work

---
### 方案二：Docker中的Ubuntu

* docker  
    - 下载  
    官网地址: https://www.docker.com/
    - 设置docker代理  
    Settings-Resources-PROXIES
    - 设置docker容器代理  
    默认地址为: C:\\Users\\Administrator\\.docker  
    编辑config.json  
    加入代理内容
    ```json
    "proxies": {
        "default": {
            "httpProxy": "http://127.0.0.1:7890",
            "httpsProxy": "http://127.0.0.1:7890",
            "noProxy": ""
        }
    },
    ```
* ubuntu
    - 搜索并拉取  
    ```
    docker search ubuntu
    docker pull ubuntu
    ```
    - 启动并映射
    ```
    docker run -i -t -v D:\xxx:/work ubuntu /bin/bash
    ```
---
### 方案三：虚拟机安装
* 下载VMWare  
    https://www.vmware.com/
* 下载Ubuntu镜像  
    https://ubuntu.com/download/desktop
* 安装启动  
    balabala...
* 建立映射  
    balabala...
---
## 编译
* 编译准备
    - 工具准备
    ```
    apt-get update
    apt-get install git
    apt-get install curl
    apt-get install wget
    apt-get install python
    ```
    - 文件准备
    ```
    cd /work
    export WORKSPACE=`pwd`
    git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
    export PATH=$PATH:$WORKSPACE/depot_tools
    cd $WORKSPACE
    mkdir webrtc
    cd $WORKSPACE/webrtc
    fetch --nohooks webrtc_android
    git branch -a
    git checkout -b 70 remotes/branch-heads/70
    gclient sync
    ```
* 编译
    ```
    cd $WORKSPACE/webrtc/src
    ./build/install-build-deps.sh
    ./build/install-build-deps-android.sh
    source ./build/android/envsetup.sh
    gn gen android/Release "--args=target_os=\"android\" target_cpu=\"arm64\" is_debug=false rtc_include_tests=false rtc_use_h264=true"
    ninja -C android/Release
    ```

---
## UE4修改

    由于某些特殊原因，项目中使用的是4.22.3版本。其它版本可以参照修改，修改主要包含——libc++、openssl、curl、websockets等几个模块，根据出现的问题，选择修改的方案。（我反正改好了，以后再添加记录）


1. 符号问题处理
2. ssl版本问题
3. curl的ssl
4. websockets的ssl


---
## WebRTC for Unreal Engine 4 on Android

* 插件的制作

        从4.24开始，EPIC对PixelStreaming作了一点升级，可以在UE4中播放这个插件输出的WebRTC流，但只支持了Windows平台。不过依然是给我们提供了示范，第一步可以将4.24版本的插件拷贝出来，再作修复和删减。

* Android平台的H264解码  

        UE4输出的流是H264编码，为了追求效率，这里我们采用Android的MediaCodec来进行H264硬解，解得的帧这时在GPU中，可以获得其Texture的ID。

* UE4中对外部纹理的渲染  

        根据抄来的插件，可以得知我们在UE4呈现的是一个材质，材质的Color来源是UMediaTexture，UMediaTexture的渲染，有Tick的Render函数，一番查找，无果。此时只能抄另一个插件，AndroidMediaPlayer，测试播放http视频流，发现不走Render。Render函数之前，就已经完成了渲染。查找到AndroidMediaPlayer的TickFetch，得知其使用FExternalTextureRegistry来注册外部纹理的更新。至此，抄抄抄，完成WebRTC for Unreal Engine 4 on Android,后续还有优化。


后话。。。鬼知道前面短短的几个东西花了我一个月时间
