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

## 7月7日

### ssh连接密码正确但被拒绝

[解决ssh服务拒绝了密码，请再试一次，但密码是正确的 - 程序员大本营 (pianshen.com)](https://www.pianshen.com/article/20051526330/)

修改/etc/ssh/sshd_config

PermitRootLogin yes

重启ssh服务 

**公钥连接**

将客户端的公钥放到服务端的.ssh/authorized_keys里面

修改/etc/ssh/sshd_config，使PubkeyAuthentication为yes。