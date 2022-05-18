[TOC]

ChromeOS
----
没错，搞了台 Chromebook！
# 1. 准备：

1. 科学上网软件
2. Google 账号
3. 一台有无线功能的设备(手机/电脑/路由器)，为初始的 Chromebook 提供可以科学上网的工具
4. [开启开发者模式](./DeveloperMode.md)(建议)否则只能从 Googleplay 商店安装
5. 如果有更换系统的打算，还要拆卸主板上的写保护螺丝

# 2. 进入系统

1. 使用一台可以科学上网的设备提供网络AP，在此我使用的无线AP创建软件是在安卓手机上的 `NetShare` ，使用方法请自行查找
2. 按照系统提示完成 Google 账号的登录
3. 此时已经可以窥得 ChromeOS 的系统全貌

# 3. 安装 Linux

目前常用的方法有
- 通过 crouton 安装 Linux
    
    Chrome OS 是基于 Linux 内核的，而 crouton 安装 Linux 是基于chroot的，用crouton安装的 Linux 是精简版本
    
- 更改 BIOS ，通过普通的方法安装 Linux

## 3.1 通过 crouton 安装 Linux
参考点击[查看](https://github.com/dnschneid/crouton)文档
1. 点击[下载](https://goo.gl/fd3zc)crouton脚本，脚本默认下载到 `~/Downloads` 文件夹里。
2. 按下`Ctrl + Alt + T` 打开 crosh ，输入 `shell`，按下回车，进入命令行可见 *用户名@设备名* : `chronos@localhost` ，如果失败请查看时候开启开发者模式
3. 键入 `sudo install -Dt /usr/local/bin -m 755 ~/Downloads/crouton` 将安装程序复制到可执行位置。这是较新版系统提供的保护措施，如果今后运行shell类文件报错也可以运行类似命令

**接下来就是疯狂报错的时刻**

4. 键入 `sudo crouton` 
   1. 如果失败出现`Check your internet connection or proxy settings (-P) and try again.]`
   2. 添加代理选项`sudo crouton -P [代理ip:port]`重试
   3. `sudo crouton -r list` 查看可以安装的系统版本
   4. `-r xenial` 选择系统以及版本，`xenial` 是`Ubuntu 16.04` 的代号
   5. `-t xfce` 选择桌面环境，还有GNOME、KDE、LXDE等
   6. `-m http://mirrors.ustc.edu.cn/ubuntu/` 重定向系统镜像，有时一些镜像会慢，再推荐[一些](./xenial_source.md)
   7. `-n name` 指定Chroot环境的名字，可以创建多个chroot，如果没有指定，默认是版本名，如xenial
   8. 其他参数
      - -k：指定储存密钥的路径
      - -u：添加安装目标
      - -e：创建一个加密的chroot环境，或者加密一个未加密的chroot环境

5. 综合如下：`sudo crouton -r xenial -t core,xorg,x11,gtk-extra,xfce,keyboard,cli-extra  -m http://mirrors.huaweicloud.com/ubuntu/ -P 192.168.49.1:8282`
6. 会发生的事情：
   1. Cronton安装需要的声卡驱动出现无法连接的情况，[可参考](https://github.com/dubuqingfeng/Chromebook-For-Chinese),来更改源码,(ps:几年前的方案，不知道能否实现。)
      
   2. 声卡驱动修改说明：
    ```
            1. 下载[Cronton](https://github.com/dnschneid/crouton)，打包下载，Download Zip

            2. 更改targets/audio文件:

                 第47行：

                 ( wget -O "$archive" "$urlbase/$ADHD_HEAD.tar.gz" 2>&1 \
                                                     || echo "Error fetching CRAS" ) | tee "$log"
                 改为：

                 ( wget -O "$archive" "http://t.cn/R46YOzM" 2>&1 \
                                                     || echo "Error fetching CRAS" ) | tee "$log"

            3. 直接运行installer/main.sh,或者make自己的crouton。
    ```
   3. 或者是声卡运行成功后发现某个软件包无法下载，让你用apt修复
   4. 全程挂载节点，才有可能成功。笑死
   5. 如果想避免安装声卡报错或者软件包的可能错误，可以尝试进安装内核(core)以及命令行(cli-extra)
7. 省略载入引导文件的过程
   1. 一遍又一遍地下载引导文件是浪费时间
   2. 构建一个引导程序 tarball： `sudo crouton -d -f ~/Downloads/mybootstrap.tar.bz2` 其他参数自行添加，必备`-r`
   3. 使用引导程序 `sudo crouton -f ~/Downloads/mybootstrap.tar.bz2`。确保还使用 `-t` 以及其他
8. 进入 Linux 环境
   1. 命令行： 键入 `sudo enter-chroot` 或者 `sudo startcli`
   2. 图形界面： xfce键入 `sudo startxfce4`
   3. 使用 `Ctrl+Alt+Shift+Back` 与 `Ctrl+Alt+Shift+Forward` 在 `Chromium OS` 和正在运行的图形 `chroot` 之间切换
9. 环境操作
   1.  删除： `sudo delete-chroot evilchroot`
   2.  编辑中的删除：`sudo edit-chroot -d evilchroot`， 上条是此条的快捷方式
   3.  编辑： `sudo edit-chroot -h` 自行查看帮助
   4.  进入：`sudo enter-chroot selete`，如前所述
10. 软件安装
    1.  code-server
    本来是想安装Linux作为编程开发工具,毕竟这台Chromebook性能不错，可是如果只安装命令行版本(比如我，在尝试中也成功安装了xfce版本的，但看着不习惯)
        1. GitHub上的地址在 https://github.com/cdr/code-server ，进去之后选择releases下载
        2. 命令行安装 `sudo dpkg -i code-*.deb`

## 3.2 更改 BIOS 安装 Linux 发行版

1. 安装mrchromebox的固件(实现UEFI引导)

   `cd; curl -LO mrchromebox.tech/firmware-util.sh`

   `sudo install -Dt /usr/local/bin -m 755 firmware-util.sh`

   `sudo firmware-util.sh`

2. 运行失败的解决方式
   1. [本地搭建服务器](./../Ubuntu/apache2.md)，然后把对应的固件先下载下来

   2. 更改脚本

      `firmware-util.sh`中：
      script_url="https://raw.githubusercontent.com/MrChromebox/scripts/master/" ==>
      script_url="http://ip/file/"

      `sources.sh` ，您需要将位于第 9 行到第 15 行的 URL(https://www.mrchromebox.tech/files/)替换成您的服务器地址:(http://ip/)

      `cd; curl -LO http://ip/file/firmware-util.sh`

      `sudo install -Dt /usr/local/bin -m 755 firmware-util.sh`

      `sudo firmware-util.sh`

   3. 利用国内的镜像下载安装[感谢wkkun.tech](https://webcache.googleusercontent.com/search?q=cache:sNrSdx932M8J:https://wkkun.tech/2020/02/03/c630-instruction/+&cd=5&hl=zh-CN&ct=clnk)
      ```shell
      cd; curl -LO wkkun.tech/main.sh && sudo bash main.sh
      ```
3. 进入脚本界面
   1. 此处会现实系统的信息
      1. 注意：Fw WP 项需为Disabled,如果是Enabled需要卸除主板上的写保护螺丝
      2. Thinkpad 13 Chromebook 写保护螺丝居然在键盘下面
   2. 选择菜单功能：一般有 `RW_LEGACY` 和 `Full ROM` 以及其他
   3. 告知刷入会无法启动ChromeOS
   4. 告知你刷机是危险行为
   5. 询问你是否要保存原版BIOS，可以插入U盘并选择盘符，保存再重新运行选择
   6. 等待下载完整镜像
   7. 确保直到看见绿色的 <font color=green face="黑体"> Full ROM firmware successfully installed/updateed </font> 再进行重启操作
   8. 如果没有！需要重新运行脚本直至完成, **要不然会导致刷写失败，变砖!**
4. 再次重启后，屏幕中央出现一个奔跑的兔子的logo
5. 屏幕底部提示：按下 `ESC` 就可进入Boot选项设置，刷写完成，至此可以安装其他操作系统
