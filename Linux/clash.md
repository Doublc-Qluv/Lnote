Clash 
======

# 1. 下载安装
## 1.1 下载 
[`clash-linux-amd64-*.gz`](https://github.com/Dreamacro/clash/releases) 

## 1.2 解压

输入 `gunzip clash-linux-amd64-*.gz -d [解压位置]`

若不指定`-d` 则解压到当前文件夹

## 1.3 运行
### 1.3.1 若为可执行文件

输入 `./clash*` 便可执行

###  1.3.2 若不可执行

添加可执行权限 
```shell
chmod +x clash*
```

## 1.4 任意位置执行
### 1.4.1 移动到`bin`

移动到 `/usr/bin` 文件夹下

```shell
sudo mv clash* /usr/bin
```
### 1.4.2 软链接到`bin` 

移动至 `/opt` 下，并软链接到 `/usr/bin`

```shell
sudo mv clash* /opt; 
sudo ln -s /opt/clash* /usr/bin/clash
```
## 1.5 运行前
### 1.5.1 文件需要

运行需要 `~/.config/clash` 或者在 `clash` 的同目录下存在 `config.yaml` 和 `Country.mmdb` 两个文件 

### 1.5.2 运行命令

命令 `./clash -d .` 表示使用当前目录下的配置文件，不加选项默认是文件同目录

## 1.6 运行时
### 1.6.1 改info

1. 在运行完 `clash`如果出现

```
INFO[0000] Start initial compatible provider GlobalTV
INFO[0000] Start initial compatible provider Proxy
INFO[0000] Start initial compatible provider Domestic
INFO[0000] Start initial compatible provider Others
INFO[0000] Start initial compatible provider AsianTV
```
2. 打开 `config.yaml` 页面，修改 `log-level` 为 `info`
3. 可以看得到输出的 info 信息了
4. 之后在浏览器中打开 `http://clash.razord.top/` 配置界面


## 1.7 配置
变更自己的配置文件 `config.yaml` 和 `Country.mmdb`
1. 一般来说，提供商会提供 `config.yaml` 替换现有的 `config.yaml`
2. 或者通过订阅链接得到文件：如果下载没有解析成功，可以在订阅地址后添加`&flag=clash`
  ```shell
  wget -O config.yaml "your subscribe link"
  ```
3. 同时获得 `Country.mmdb`：
  ```shell
  wget -O Country.mmdb "https://www.sub-speeder.com/client-download/Country.mmdb"
  ```
  下载失败可以用本仓库的备用版本
  ```shell
  wget -O Country.mmdb "https://github.com/Doublc-Qluv/Lnote/releases/download/Linux/Country.mmdb"
  ```
4. 如果无法完成订阅请检查 clash 版本 `clash -v`
   - 在1.0版本时，clash [更新了api](https://lancellc.gitbook.io/clash/whats-new/highlight)

   - API changed
     https://github.com/Dreamacro/clash/wiki/Breaking-Changes-in-1.0.0
     - Proxy --> proxies
     - Proxy Group --> proxy-groups
     - Rule --> rules
     - proxy-provider --> proxy-providers
     - rule-provider --> rule-providers
     - Final --> Match
     - SOURCE-IP-CIDR  --> SRC-IP-CIDR
   - 在 `config.yaml` 中更改后重试

# 2. 从软件仓库安装

## 2.1 从 `Arch Linux` 的 官方仓库里安装
```shell
sudo pacman -S clash

# 或者

yay -S clash
```
## 2.2 暂没发现