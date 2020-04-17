# HomeLede 版本说明
+ 基于Lede OpenWrt 及来自Lienol和若干自行维护的软件包（Feed）
+ 结合家庭x86软路由场景需要定制
+ 按照家庭应用场景对固件及软件进行测试（x86），通过后发布

对家庭路由高频功能进行了测试（x86软路由），保证可用。

## 固件内置功能
+ 支持UPnP（为BT、EMULE，家用摄像头、XBOX、PS4提供支持）
+ 支持CIFS文件共享协议（路由直接挂载NAS、Samba、Windows文件夹，通过cifs.mount实现，提供图形化挂载工具）
+ 支持自动挂载空闲分区、U盘以及自动向局域网内部共享（通过Samba实现）
+ 支持单线/多线并发多拨（提升上行带宽，提高从因特网获取家庭文件速度）
+ 支持多拨负载均衡
+ 内置综合DNS解决方案：去广告+国内域名加速解析+ 抗污染 + 速度优选 与PSW无缝集成
+ 支持DDNS（可以通过域名随时获得家庭路由器IP）
+ 支持SSH远程访问（从因特网连接路由器，传输文件，任意访问内网，端口转发等等）
+ 基于IpSec、IKev2、ZeroTier VPN方案（苹果，安卓手机可无需安装额外软件连入家庭局域网）
+ 支持远程唤醒（WOL，从因特网连入路由器启动家中电脑）
+ 支持定时唤醒（Time WOL，定时启动家庭设备，配合自动关机实现定时运行）
+ 支持全功能Docker，可自由扩展功能（可安装目前还没有移植到OpenWrt上的软件）
+ 支持SFTP（可通过常见SSH客户端随意向路由传输文件，而不需要通过Web界面）
+ 预置OpenVMTools（优化在虚拟化环境中运行速度）
+ 支持百度网盘远程下载（使用CIFS挂载NAS后可以远程下载网盘内容到NAS）
+ 提供Aria2下载工具（远程或者本地下载普通链接，磁力链，BT等全部主流格式，挂载NAS后可直接下载到NAS）
+ 提供视觉效果较好的皮肤
+ 其他必备功能（具体请查看固件下载地址中的内置软件截图）

感谢Lean（coolsnowwolf），Lienol，CTCGFW等等作者。

PS：内置综合DNS解决方案说明请见 https://www.cnblogs.com/zlAurora/p/12501185.html

==============================================================================

## 编译说明

注意：
1. **不**要用 **root** 用户 git 和编译！！！
2. 国内用户编译前最好准备好梯子
3. 默认登陆IP 192.168.1.1, 密码 password


编译前：
1. 首先装好 Ubuntu 64bit，推荐  Ubuntu 18 LTS x64
2. 至少30G空闲硬盘空间
3. 2G以上内存，建议4G

编译时:
1. 更新apt-get包信息，命令行输入
`sudo apt-get update`

2. 安装编译依赖包，命令行输入
`sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3.5 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf`

3. `git clone https://github.com/xiaoqingfengATGH/HomeLede.git homeLede`命令下载好源代码，然后 `cd homeLede` 进入目录

4.  `./prepareCompile.sh`

5. `make download V=s` 下载dl库（国内请尽量全局科学上网,如果程序下载失败，也可以提取网址自行下载后放入dl文件夹，此文件夹通常不需要删除）

6. `make menuconfig`  配置软件包

7. `make -j1 V=s` （-j1 后面是线程数。第一次编译推荐用单线程，国内请尽量全局科学上网）即可开始编译你要的固件了。

编译成功后，再次编译可以启动多线程编译。如4核心8线程i7上开启16线程使用`make -j16 V=sc`

本套代码保证肯定可以编译成功。里面包括了 R20 所有源代码，包括 IPK 的。

去广告订阅地址默认内置来自以下源，如有去广告的误杀漏杀问题可以到这里报告：

https://github.com/privacy-protection-tools/anti-AD

## 固件下载
如需直接编译完成的固件，请访问Google网盘
链接：https://drive.google.com/open?id=1iUDsgh1y5qouP48V61aTsswi3IekscKk