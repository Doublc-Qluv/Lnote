# 搭建简单http服务器
[参考](https://blog.csdn.net/qq_30624591/article/details/118573780)

1. 安装apache2
    ```shell
    sudo apt-get update
    sudo apt-get install apache2
    ```
2. 重启服务 `sudo /etc/init.d/apache2 restart`
3. 查看本机ip `ifconfig`， 并使用ip地址访问本机
4. 建立一个共享文件夹 `cd; mkdir http_source`
5. 在/var/www/html目录下建立一个文件夹软链接（管理的文件目录）
    ```
    cd /var/www/html 
    sudo ln -sf ~/http_source file
    ```
6. 输入ip/file，就可以访问该文件夹了