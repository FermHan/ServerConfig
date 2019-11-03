## 配置IP

##### 查询路由器映射：

输入路由器IP地址：`XXX.XXX.XXX.XXX`登录后，点击NAT配置，点击内部服务器，可以看到网络映射情况。

![](https://raw.githubusercontent.com/FermHan/tuchuang/master/20191103134849.png)

重装系统的话，内外网IP映射已在路由器上设置好。所以我们在主机上配置IP的适合，无需管外网IP，全都填内网IP即可。

之前有个Excel表中有些IP是错误的，比如我配置的19就与路由器中设置的不一致。

如图，我查到的外网端口9019和9119映射到了内网IP的192.168.10.19的3389和22端口。这两个端口无需配置，一般安装ssh和远程桌面后默认的端口就是。

- 22端口是ssh的端口。
- 3389端口是远程桌面的端口。

##### 使用`ifconfig`命令查看网卡名称

![](https://raw.githubusercontent.com/FermHan/tuchuang/master/20191103134440.png)

##### 配置网卡

如图我查到的网卡名称是eno1，然后配置网卡`sudo vim /etc/network/interfaces `

```SH
auto eno1
iface eno1 inet static
address 192.168.10.19
netmask 255.255.255.0 # 通用
gateway 192.168.10.1 # 与address只有最后一个不一样
dns-nameser 192.168.10.1 #这项比较难搞
```

上面配置的是静态IP，否则每次重启IP都会改变。

> 注意：DNS地址如果在/etc/resolv.conf里配置当重启时DNS地址将会被重置，resolv.conf的DNS地址是根据/etc/resolvcon/resolv.conf.d/head文件内容更新生成的。
>
> 所以要永久更新DNS地址可以在 `/etc/network/interfaces`中写入`dns-nameserver XX.XX.X.X`来配置；
>
> 也可以`sudo vi /etc/resolvconf/resolv.conf.d/head`中写入`nameserver XX.XX.X.X`

##### 重启网卡

`sudo /etc/init.d/networking restart`

此时就能上网了。

## 配置ssh

```sh
sudo apt-get insatll openssh-server
sudo /etc/init.d/ssh start
# sudo /etc/init.d/ssh restart
# sudo /etc/init.d/ssh stop
```

修改ssh端口（一般不需要进行）

```SH
sudo vim /etc/ssh/sshd_config
Port 22改为想要的端口
```

## 配置远程桌面：

 https://blog.csdn.net/hancoder/article/details/102882153 

