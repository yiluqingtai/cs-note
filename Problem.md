## 6月9日

### 虚拟机无法ping通主机

参考：[防火墙设置：虚拟机ping不通主机，但是主机可以ping通虚拟机_IT人的日常-CSDN博客](https://blog.csdn.net/u014594922/article/details/53426225)

解决方案：控制面板-防火墙-高级设置-入站规则-文件和打印机共享（回显请求-ICMPv4，公用）-启用规则

## 6月18日

### Jetbrain软件激活

https://shimo.im/docs/WY3hd8Jt8KHgvVty/read

### Linux环境变量配置

[【linux】Linux下环境变量（.bash_profile和.bashrc的区别） - 望着小月亮 - 博客园 (cnblogs.com)](https://www.cnblogs.com/triple-y/p/11107133.html)

（1）修改/etc/profile文件

推荐使用这种方法，因为所有用户的shell都有权使用这些环境变量，缺点是可能会给系统带来安全性问题。 这里是针对所有的用户的,所有的shell;

（2）修改.bashrc文件

这种方法更为安全，它可以把使用这些环境变量的权限控制到用户级别,这里是针对某一个特定的用户，如果需要给某个用户权限
使用这些环境变量，只需要修改其个人用户主目录下的.bashrc文件就可以了。

（3）git代理配置

```shell
# 方法一
git config --global --edit
# 方法二
vim ~/.gitconfig
# 方法三
git config --global https.proxy ip:port
git config --global http.proxy ip:port
```

（4）网络代理配置

```shell
export http_proxy=ip:port
export https_proxy=ip:port
```

## 7月12日

### 主机无法访问虚拟机服务

[(6条消息) 本地主机客户端访问不了VMware虚拟机里的服务器_jee0520的博客-CSDN博客_主机无法访问虚拟机服务器](https://blog.csdn.net/jee0520/article/details/80708679)

linux防火墙的问题：

```
iptables -F
iptables -P INPUT ACCEPT
```

## 7月20日

### ubuntu文件系统扩容

@时间：2021年1月7日

@目标：将ubuntu的根目录扩容到100G，并将home目录单独挂载到50G的磁盘上。

@环境：Vmware虚拟机，ubuntu 18.04系统

**1 信息收集**

**1.1 分区表类型和文件系统类型**

分区表类型查询：

```shell
$ fdisk -l [/dev/sda]
Disklabel type: dos/msdos # MBR分区表
Disklabel type: gdp
```

文件系统查询：

```shell
$ df -T
... Type ...
... ext4 ... # ext4支持文件系统容量放大和缩小，xfs仅支持放大，其他系统不支持
```

**1.2 LVM软件安装**

LVM软件：ubuntu18.04没有自带lvm2，centos7有。

```shell
$ apt install lvm2
```

**2 增加物理磁盘**

在vmware中添加100G的磁盘；（如果之前磁盘就由lvm管理，并且还有剩余未分配空间，直接扩展VG/LV）

重启虚拟机，查看检测到的磁盘：

```shell
$ lsblk
sdb ...
```

**3 磁盘分区和创建逻辑卷**

磁盘分区

```shell
$ fdisk /dev/sdb
$ Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): e
Partition number (1-4, default 1):
First sector (2048-209715199, default 2048):
Last sector, +sectors or +size{K,M,G,T,P} (2048-209715199, default 209715199): +50G

Created a new partition 1 of type 'Extended' and of size 50 GiB.

$ Command (m for help): p
Disk /dev/sdb: 100 GiB, 107374182400 bytes, 209715200 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x677bdb16

Device     Boot Start       End   Sectors Size Id Type
/dev/sdb1        2048 104859647 104857600  50G  5 Extended

$ Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

刷新并查看

```shell
$ partprobe
$ cat /proc/partitions
...
... sdb
...
```

建立逻辑卷

```shell
$ pvcreate # 建立物理卷
$ vgcreate vgnew /dev/sdb1 # 建立卷组vgnew
$ lvcreate -L 49G -n lvnew vgnew # 建立逻辑卷lvnew，设为正好50G可能不能通过
$ lsblk # 查看逻辑卷 /dev/sdb1/vgnew-lvnew
```

**4 备份家目录**

```shell
$ cp -r /home/[your home directory] [any other location in your system, such as /data/] & # 当前磁盘空间不够的话，需要先创建一个逻辑卷，格式化后挂载到某个目录下，备份家目录到该位置
$ rm -rf /home/[your home directory]
```

**5 格式化和挂载**

格式化

```shell
$ mkfs.ext4
```

设置启动挂载

~~~shell
$ vim /etc/fstab
```/etc/tab
/dev/mapper/vgnew-lvnew /home ext4 defaults 0 0 # 添加这一行，设置启动挂载
```/etc/tab
$ mount -a
~~~

将家目录拷贝回来

```shell
$ cp -r /data/[your home directory] /home
```

附录

1）更改磁盘分区的类型代号(type code)不会丢失文件系统中已存在的文件。（只测试了Linux->Linux LVM）

2）在为使用LVM管理的磁盘中创建物理卷会擦除磁盘中原有的所有数据。

3）查看文件夹大小：`du -sh [filename]`
