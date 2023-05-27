在`Ubuntu`中的`tips`

[apache2](./apache2)


## snap
一种包管理工具

安装路径统一在`/snap`中

```bash
snap list # 查看已安装的包

sudo snap search xxx　# 查找要安装的包
sudo snap install xxx # 安装包
sudo snap remove xxx # 移除要安装的包

```

- 遇到的问题 1: `snap错误has install-snap change in progress`
  - 场景: 在安装时遇到
  - 原因: 之前的安装错误终止，使得当前的安装无法进行
  - 解决: 
  ```bash
  snap changes
  ```
  将在`Doing`状态的活动的`ID`剔除
  ```bash
  sudo snap abort ID
  ```
- 遇到的问题 2: `更新snap-store`
  - 场景: 在开机后，系统中常出现 `"unable to update snap store"` 的提示
  - 原因: `snap-store` 无法自动更新
  - 解决: 
  ```bash
  sudo snap refresh snap-store
  ```
  
  输入后出现错误，显示 
  
  ```bash
  错误：cannot refresh "snap-store": snap "snap-store" has running apps
         (snap-store), pids: 1842
  ```
  ```bash
  sudo kill pids # 杀死该进程
  ```
  ```bash
  sudo snap refresh snap-store # 重新输入
  ```
  - 未解决: `自动连接　snap "snap-store" 的符合条件的插头和插槽` 一直循环
  - 补充: 以上需要时间，耐心等待