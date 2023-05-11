>> Linux 

#### 常用操作

```
(1) linux 磁盘空间查看
    du -sh /data       该目录下的占用空间
    df -h              整个磁盘占用
    sudo du -sh ./ui*  查看ui目录占用空间

```

#### 网络相关

```
(1) 查看网络端口
    sudo netstat -anp  查看网络端口使用情况

(2) 查看是否禁用ping
    /proc/sys/net/ipv4/icmp_echo_ignore_all
    1禁用
    0开启

(3) 查看是否开启路由回查
    cat /proc/sys/net/ipv4/conf/Vlan_00/rp_filter
    修改命令：
    sysctl -w net.ipv4.conf.all.rp_filter=0

(4) linux 路由表文件
    /etc/data/iproute2/rt_tables
    
    
    
    
    
    
```



