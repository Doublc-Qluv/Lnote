# xenial cn官方源

更改位置 /etc/apt/source.list

一般会注释源码项

```list
deb http://cn.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse
deb http://cn.archive.ubuntu.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://cn.archive.ubuntu.com/ubuntu/ xenial-updates main restricted universe multiverse
deb http://cn.archive.ubuntu.com/ubuntu/ xenial-backports main restricted universe multiverse
##测试版源
#deb http://cn.archive.ubuntu.com/ubuntu/ xenial-proposed main restricted universe multiverse
# 源码
#deb-src http://cn.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse
#deb-src http://cn.archive.ubuntu.com/ubuntu/ xenial-security main restricted universe multiverse
#deb-src http://cn.archive.ubuntu.com/ubuntu/ xenial-updates main restricted universe multiverse
#deb-src http://cn.archive.ubuntu.com/ubuntu/ xenial-backports main restricted universe multiverse
##测试版源
#deb-src http://cn.archive.ubuntu.com/ubuntu/ xenial-proposed main restricted universe multiverse
```




# 服务器列表
```很多网址已变更，自行搜寻
可将http://cn.archive.ubuntu.com/ubuntu/ 替换为下列任意服务器：
Ubuntu官方（欧洲，国内较慢，无同步延迟）
http://archive.ubuntu.com/ubuntu/
Ubuntu官方中国（目前是阿里云）
http://cn.archive.ubuntu.com/ubuntu/
网易（广东广州电信/联通千兆双线接入）
http://mirrors.163.com/ubuntu/
搜狐（山东联通千兆接入）
http://mirrors.sohu.com/ubuntu/
阿里云（北京万网/浙江杭州阿里云服务器双线接入）
http://mirrors.aliyun.com/ubuntu/
腾讯
http://mirrors.cloud.tencent.com/ubuntu/
华为
http://mirrors.huaweicloud.com/ubuntu/
首都在线科技
http://mirrors.yun-idc.com/ubuntu/
贝特康姆（江苏常州电信）
http://centos.bitcomm.cn/ubuntu/
CNNIC
https://mirrors.cnnic.cn/ubuntu/
开源社
http://mirror.kaiyuanshe.cn/ubuntu/


教育网
以下服务器有教育网接入，推荐教育网用户使用IPv6：
中科大LUG（合肥，电信/联通/移动/教育网自动分流，同时也是Deepin官方）
https://mirrors.ustc.edu.cn/ubuntu/ （v4/v6）http://mirrors4.ustc.edu.cn/ubuntu/ （v4）http://mirrors6.ustc.edu.cn/ubuntu/ （v6）
中科院OpenCAS
http://mirrors.opencas.cn/ubuntu/
清华TUNA（教育网核心节点百兆接入，已计划提高到千兆）
http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ （v4/v6）http://mirrors.4.tuna.tsinghua.edu.cn/ubuntu/ （v4）http://mirrors.6.tuna.tsinghua.edu.cn/ubuntu/ （v6）
中国地质大学开源镜像站，中国地质大学点石团队
http://mirrors.cug.edu.cn/ubuntu/ （v4/v6）http://mirrors.cug6.edu.cn/ubuntu/ （v6）
北京交通大学更新服务器（教育网/电信百兆接入），由北交信息中心赞助
http://mirror.bjtu.edu.cn/ubuntu/ （v4/v6）http://mirror6.bjtu.edu.cn/ubuntu/ （v6）
北京理工大学
http://mirror.bit.edu.cn/ （v4/v6）http://mirror.bit6.edu.cn/ubuntu/ （v6）
北京化工大学
http://ubuntu.buct.cn/ubuntu/ （v4/v6）http://ubuntu.buct6.edu.cn/ubuntu/ （v6）
北京外国语大学
https://mirrors.bfsu.edu.cn/ubuntu/ （v4/v6）
天津大学，天津大学信息与网络协会和天津大学自由软件联盟（校外限IPv6访问）
http://mirror.tju.edu.cn/ubuntu/ （v4/v6）http://mirror.tju6.edu.cn/ubuntu/ （v6）
南开大学，限教育网访问
http://ftp.nankai.edu.cn/ubuntu/
山东理工大学，限校内访问
http://mirrors.sdutlinux.org/ubuntu/
东北大学
http://ftp.neu.edu.cn/mirrors/ubuntu/ （v4/v6）http://ftp.neu6.edu.cn/mirrors/ （v6）
哈尔滨工业大学
http://run.hit.edu.cn/ubuntu/ （v4/v6）http://run6.hit.edu.cn/ubuntu/ （v6）
吉林大学，由吉林大学网络中心维护
http://mirrors.jlu.edu.cn/ubuntu/
大连理工大学
http://mirror.dlut.edu.cn/ubuntu/
上海交通大学（教育网千兆接入，联通/电信线路情况不详）
http://ftp.sjtu.edu.cn/ubuntu/ （v4/v6）http://ftp6.sjtu.edu.cn/ubuntu/ （v6）
上海大学
http://mirrors.shuosc.org/ubuntu
上海科技大学
http://mirrors.geekpie.org/ubuntu
南京大学，由人工微结构科学与技术协同创新中心‧南京微结构国家实验室‧南京大学网络信息中心维护
http://mirrors.nju.edu.cn/ubuntu/
南京师范大学，限校内访问
http://mirrors.njnu.edu.cn/ubuntu/
南京邮电大学
http://mirrors.njupt.edu.cn/ubuntu/
南京信息工程大学，限教育网访问
http://mirrors.duohuo.org/ubuntu/
浙江大学，由浙江大学Linux用户组维护
http://mirrors.zju.edu.cn/ubuntu/
华中科技大学，由华中科技大学网络与计算中心维护
http://mirrors.hust.edu.cn/ubuntu/
华中科大联创团队，由华中科技大学启明学院的联创团队维护
http://mirrors.hustunique.com/ubuntu/
厦门大学，由厦门大学信息与网络中心维护
http://mirrors.xmu.edu.cn/ubuntu/archive/ （v4/v6）http://mirrors.xmu6.edu.cn/ubuntu/ （v6）
中山大学，由中山大学网络与信息技术中心维护
http://mirror.sysu.edu.cn/ubuntu/
华南农业大学，由华南农业大学红满堂工作室维护
https://mirrors.scau.edu.cn/ubuntu/
电子科技大学（位于成都），由电子科技大学学生宿舍网络管理委员会维护，仅包含Ubuntu镜像
http://ubuntu.dormforce.net/ubuntu/
重庆大学，由重庆大学蓝盟维护
http://mirrors.cqu.edu.cn/ubuntu/
西安交通大学，由西安交通大学众享社维护
http://ubuntu.xjtuns.cn/ubuntu/
西安电子科技大学，限教育网访问
http://ftp.xdlinux.info/ubuntu/
西北农林大学，
https://mirrors.nwafu.edu.cn/ubuntu/
兰州大学，由兰州大学开源社区维护
http://mirror.lzu.edu.cn/ubuntu/


大陆地区以外
香港中文大学更新服务器，由香港中文大学信息技术服务处维护
http://ftp.cuhk.edu.hk/pub/Linux/ubuntu
香港01link更新服务器，由香港联达网络服务有限公司维护
http://ubuntu.01link.hk
香港uhost更新服务器，由香港互联科技有限公司维护
http://ubuntu.uhost.hk
台湾
http://tw.archive.ubuntu.com/ubuntu
```