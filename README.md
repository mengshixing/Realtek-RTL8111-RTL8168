# Realtek-RTL8111-RTL8168
处理联想电脑网卡驱动问题 ubuntu18.04 LTS server

## 坑爹的联想电脑重启之后ifconfig -a 只有lo ## 
* 瞅瞅 lspci | grep -i eth 网卡还在, 型号是RTL8111/8168B
* 去官网下载了驱动包 详见本仓库 r8168-8.047.01.tar.bz2
* 拷贝到U盘,mount上,随便拷贝到一个文件夹解压
* 最好sudo到root账号上, make clean modules 然后 make install 然后  depmod -a
* make install 时候可能会报错缺少包依赖 libelf-dev(它还依赖zlib1g-dev),本仓库均已下载,拷贝之后dpkg -i 包名即可
* 驱动安装成功后重启一下 modprobe r8168  有可能报错required key not available
* 处理方式为联想的话开机按f2 进bios然后 进入 secure boot 关掉即可
* lsmod |grep r8168 查看是否成功
* ifconfig a 看看除了lo之外多出来一个enp4s0之类的就可以了
* 配置静态ip可以用netplan 这个会默认用systemd-networkd 也支持NetworkManager 
