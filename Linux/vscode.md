VSCode
=====
# 1. 安装

[下载地址](https://code.visualstudio.com/#alt-downloads)

ps.国内下载缓慢的解决方式：将下载地址中: `az764295.vo.msecnd.net` ，更换成 `vscode.cdn.azure.cn` (全系统通用)

## 1.1 通用方法：利用tar.gz包安装vscode

1. 首先官网去下载稳定版安装包vscode官网
code-stable-xxxx.tar.gz

2. 解压安装包到/opt/目录
    ```shell
    sudo tar -zxvf code-stable-1562627471.tar.gz -C /opt/
    ```
3. 加上执行权限
    ```shell
    sudo chmod +x /opt/VSCode-linux-x64/code
    ```
4. 加入系统环境
   ```shell
   ln -s /opt/VSCode-linux-x64/code /usr/local/bin/code
   ```
5. code就可以直接启动了

6. 桌面快捷键

   1. 在/usr/share/applications/下创建visualstudiocode.desktop文件

    ```shell
    vim /usr/share/applications/visualstudiocode.desktop
    ```
   2. 拷贝如下内容：
    ```
    [Desktop Entry]
    Name=Visual Studio Code
    Comment=Multi-platform code editor for Linux
    Exec=/opt/VSCode-linux-x64/code
    Icon=/usr/share/icons/code.png
    Type=Application
    StartupNotify=true
    Categories=TextEditor;Development;Utility;
    MimeType=text/plain;
    ```
   3. 图标
    ```shell
    sudo cp /opt/VSCode-linux-x64/resources/app/resources/linux/code.png /usr/share/icons/
    ```

## 1.2 Debian & Ubuntu

1. 下载` .deb` 包

2. 输入命令

    ```shell
    sudo dpkg -i code-*.deb
    ``` 
3. 或可直接点开`.deb`安装

## 1.3 RedHat & Fedora & SUSE

1.  下载 .rpm 包

2.  输入命令
    ```shell
    sudo rpm -ivh code-*.rpm 
    ```

3. 注意依赖安装

    ```shell
    sudo yum install libXScrnSaver
    ```

# 2. 使用注意

## 2.1 打开黑屏
- 虚拟机里出现的打开黑屏问题：可能是由于虚拟机的gpu加速造成的。修改操作如下：
  - 如使用命令行打开将命令修改为
  ```bash
  code --disable-gpu
  ```
  - 如使用图标等快捷方式启动，以ubuntu为例，在启动图标中的两处加上`--disable-gpu`
  ```bash
  cd  /usr/share/applications
  sudo vim code.desktop
  ```
  ```vim
  [Desktop Entry]
  Name=Visual Studio Code
  Comment=Code Editing. Redefined.
  GenericName=Text Editor
  Exec=/usr/share/code/code --disable-gpu --unity-launch %F
  Icon=com.visualstudio.code
  Type=Application
  StartupNotify=false
  StartupWMClass=Code
  Categories=Utility;TextEditor;Development;IDE;
  MimeType=text/plain;inode/directory;application/x-code-workspace;
  Actions=new-empty-window;
  Keywords=vscode;

  [Desktop Action new-empty-window]
  Name=New Empty Window
  Exec=/usr/share/code/code --disable-gpu --new-window %F
  Icon=com.visualstudio.code
  ```

- 或者考虑在虚拟机软件中关闭`gpu加速`或者`3d加速`

## 2.2 清理空间

可以尝试删除VScode中ipch文件, 其位于:

```sh
/home/用户名/.cache/vscode-cpptools/ipch
```

- **Cache**：在计算机存储系统的层次结构中，介于中央处理器和主存之间的高速小容量存储器。它和主存储器一起构成一级的存储器。高速缓存存储器和主存存储器之间信息的调度和传送是由硬件自动进行的。

- **Ipch**：这些文件是Visual Studio用来保存预编译版的头文件和Intellisense。如果删除后，重新加载项目会重建这些文件，但VSCode中设定范围后就不会产生超过这个数的缓存大小。
  - ipch文件内包含缓存的预编译头文件（PCH），vscode使用的时间越长，那么这个文件夹内的缓存就越多，最终会造成较大的内存占用。当我们不用来运行很大的文件时，只是利用它来敲代码，用不到预编译头文件时可以关闭这个功能。

- 操作如下
在VSCode菜单栏中 `文件->首选项->设置` `(ctrl+，)`，然后搜索`C_Cpp.intelliSenseCacheSize`,修改其默认值`5120`为`512`,此时vscode会直接重置`ipch`文件夹