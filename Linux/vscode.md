# 1-安装vscode

[下载地址](https://code.visualstudio.com/#alt-downloads)

ps.国内下载缓慢的解决方式：将下载地址中一级域名: `az764295.vo.msecnd.net` ，更换成 `vscode.cdn.azure.cn` (全系统通用)

## 通用方法：利用tar.gz包安装vscode

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

## Debian & Ubuntu

1. 下载 .deb 包

2. 输入命令

    ```shell
    sudo dpkg -i code-*.deb
    ``` 

## RedHat & Fedora & SUSE

1.  下载 .rpm 包

2.  输入命令
    ```shell
    sudo rpm -ivh code-*.rpm 
    ```

3. 注意依赖安装

    ```shell
    sudo yum install libXScrnSaver
    ```

# 2-使用注意

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
  ```vi
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