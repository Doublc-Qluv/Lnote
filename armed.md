[TOC]

# 1. Software
## 1.1 Chrome
对于新建的chrome，设置百度为默认搜索引擎
- 搜索 搜索引擎(search engine)
- 管理搜索引擎(Manage search engines)
- 没有的话，添加即可，注意url的写法 "https://www.baidu.com/s?ie=${inputEncoding}&wd=%s"
- 设置其为默认搜索引擎即可


## 1.2 git

### 1.2.1 一般git操作
```shell
git init

git add .

git commit -m 'commit message'

git remote add origin git@github.com:xxx.git
//使用ssh将此项目添加到远程github上
 
git branch -M main
//从2020年起，将master改为main分支（实际使用master也暂时不影响）

git push -u origin main
```
中间可能会提示，让你配置用户名和邮箱，配置一下就行了


### 1.2.2 一台电脑上配置git的不同远端仓库
以`github & gitee`为例 方法来源 [itchuan.net（钏）](https://blog.csdn.net/sinat_37390744/article/details/109023834)
- 应知应会
  - 配置全局email和name
  ```shell
  git config --global user.name "yourname"
  git config --global user.email "youremail@address"
  ```
  - 删除原有全局配置
  ```shell
  git config --global --unset user.name
  git config --global --unset user.email
  ```
  - 复制公钥到远端网站帐号
  - 测试公钥是否添加成功(例如github)
  ```shell
  ssh -T git@github.com
  ```
- 生成配置公私钥
  - 生成目的远端公私钥(找到本机`.ssh`地址)
    ```shell
    ssh-keygen -t rsa -f ~/.ssh/id_rsa.github -C "youremail@github"
    ssh-keygen -t rsa -f ~/.ssh/id_rsa.gitee -C "youremail@gitee"
    ```
  - 在`.ssh`文件夹下，新建并将以下内容写入配置文件`config`
    ```config
    Host github.com
        HostName github.com
        User git 
        IdentityFile ～/.ssh/id_rsa.github
    
    Host gitee.com
        Port 22
        HostName gitee.com
        User git
        IdentityFile ～/.ssh/id_rsa.gitee
    ```
    ps`.ssh`路径要写全 win/mac/linux

### 1.2.3 `.git`文件夹太大的解决方法

方法来源[Intopass](https://www.zhihu.com/question/29769130/answer/45546231)
1. 完全重建版本库
```shell
$ rm -rf .git
$ git init
$ git add .
$ git cm "first commit"
$ git remote add origin <your_github_repo_url>
$ git push -f -u origin master
```

push不上去的话考虑添加`push --force`

2. 有选择性的合并历史提交
```shell
$ git rebase -i <first_commit>
```
```
会进入一个如下所示的文件
  1 pick ba07c7d add bootstrap theme and format import
  2 pick 7d905b8 add newline at file last line
  3 pick 037313c fn up_first_char rename to caps
  4 pick 34e647e add fn of && use for index.jsp
  5 pick 0175f03 rename common include
  6 pick 7f3f665 update group name && update config

将想合并的提交的pick改成s，如
  1 pick ba07c7d add bootstrap theme and format import
  2 pick 7d905b8 add newline at file last line
  3 pick 037313c fn up_first_char rename to caps
  4 s 34e647e add fn of && use for index.jsp
  5 pick 0175f03 rename common include
  6 pick 7f3f665 update group name && update config

这样第四个提交就会合并进入第三个提交。
等合并完提交之后再运行
```
```shell
$ git push -f
$ git gc --prune=now
```
## 1.3 Anaconda
### 1.3.1 更新导致不兼容
使用anaconda创建一个新的环境，执行“conda create -n xx”，结果出现了

  “CondaHTTPError: HTTP 000 CONNECTION FAILED for url \<https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/win-64/current_repodata.json\>”

之前的没有问题，可能是设置更新导致的不兼容

解决方法：
- 设置.condarc
```condarc
ssl_verify: true
show_channel_urls: true
channels:
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
  - bioconda
  - conda-forge
  - r
#  - defaults
```
- 一般方法，在设置完main与free之后更新就会好，
- 我的问题主要出现在`main`文件夹，一般conda的逻辑就是连接超时的情况下，就会这样判定，所以先换个网络
- 上述不行的情况，将`channels`中的`https`改为`http`
- 更新方式：
```bash
conda update --all #在base环境下
conda update conda
```
- 当然，不做单独update也是可以的，毕竟base环境里不放啥东西

- `tip`新发现的源,应该是tuna的副本,but接入下载是真的快
```
channels:
  - defaults
# show_channel_urls: true
default_channels:
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/main
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/r
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.bfsu.edu.cn/anaconda/cloud
  msys2: https://mirrors.bfsu.edu.cn/anaconda/cloud
  bioconda: https://mirrors.bfsu.edu.cn/anaconda/cloud
  menpo: https://mirrors.bfsu.edu.cn/anaconda/cloud
  pytorch: https://mirrors.bfsu.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.bfsu.edu.cn/anaconda/cloud
```

## 1.4 VSCode

- 国内下载缓慢的解决方式：将下载地址中:(az764295.vo.msecnd.net)，更换成(vscode.cdn.azure.cn)

[更多](./Linux/vscode.md)

## 1.5 Qt
- 下载开源版:[https://download.qt.io/official_releases/qt/](https://download.qt.io/official_releases/qt/)
- 给下载的文件以可执行权限，(chmod +x qt*)
- 修改配置文件(sudo vi  /usr/lib/x86_64-linux-gnu/qt-default/qtchooser/default.conf)

## 1.6 Clash

[更多](./Linux/clash.md)

# 2. System
## 2.1 Ubuntu

### 2.1.1 配置
#### 2.1.1.1gnome 鼠标以及游标的大小

|默认|中等|很大|更大|最大|
|:--:|:--:|:--:|:--:|:--:|
|24|32|48|64|96|

```bash
# 获得大小
$ gsettings get org.gnome.desktop.interface cursor-size
# 改变大小
$ gsettings set org.gnome.desktop.interface cursor-size [sizeInPixels]
```
### 2.1.2 清理空间

推荐工具: `ncdu`


在/var/log/journal/垃圾日志文件，可以看到他的内存占用是比较大的，那么我们可以通过如下命令来清除这些日志文件

journalctl --disk-usage        # 检查日志大小
sudo journalctl --vacuum-time=1w    # 只保留一周的日志

sudo journalctl --vacuum-size=500M    # 只保留500MB的日志

rm -rf /var/log/journal/askd342fh35aewfhagf67iuro1（垃圾文件）    # 直接删除/var/log/journal/目录下的日志文件

du -sh ~/.cache/thumbnails       # 检查缩略图缓存的大小
rm -rf ~/.cache/thumbnails/*     # 清除缩略图缓存




## 2.2 MAC

### 2.2.1 更换Homebrew源（以中科大源为例）
```shell
替换brew.git:
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

替换homebrew-core.git:
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```
### 2.2.2 换回官方源
```shell
重置brew.git:
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git

重置homebrew-core.git:
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core.git
```
### 2.2.3 换源完更新
```shell
brew update
```

## 2.3 Manjaro

### 2.3.1初始化设置
选择下载源：
```bash
sudo pacman-mirrors -i -c China -m rank
```
更新源列表
```bash
sudo pacman-mirrors -g
```
更新pacman数据库并全面更新系统
```bash
sudo pacman -Syyu
```

安装软件示例：安装ARU包管理工具
```bash
sudo pacman -S yay
```

更新系统出现提示：无法锁定数据库，
```shell
#删除数据库缓存
sudo rm -rf /var/lib/pacman/db.lck

#重新更新
sudo pacman -Syyu
```

# 3. Programming

## 3.1 gcc
### 3.1.1 pthread

在带有`<pthread.h>`库进行编译时，一般要连接动态链接库 `libpthread.so`,即在gcc编译时，在末尾添加`-pthread`

## 3.2 python 
### 3.2.1 jupyter notebook
在jupyter notebook中切换不同环境的内核
需要在当前需要运行的环境中安装 ipykernel
```bash
#安装 ipykernel
conda install ipykernel
#链接内核
python -m ipykernel install --user --name [envname] --display-name "envname"
```