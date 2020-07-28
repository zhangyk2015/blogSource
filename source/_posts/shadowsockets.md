---
title: Shadowsocks搭建配置
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-28 16:35:39
password: 
summary: Shadowsocks在Ubuntu服务器的搭建配置
tags: 
- s科学上网
- shadowsocks
categories: 
- 服务器相关
- 
---
<div style="padding-bottom: 24px;">Shadowsocks搭建配置</div>
</div>

*   `apt install python python-pip python-m2crypto`
*   安装shadowsocks
    *   `pip install shadowsocks`
*   配置文件/etc/shadowsocks/config.json
    *   单用户  ```json
        {  
        "server":"ip",  
        "server_port":8888,  
        "local_address": "127.0.0.1",  
        "local_port":1080,  
        "password":"123456789",  
        "timeout":300,  
        "method":"rc4-md5",  
        "fast_open": true,  
        "workers": 1  
        }  ```

    *   多用户 ```json
        {  
        "server":"ip",  
        "local_address": "127.0.0.1",  
        "local_port":1080,  
        "port_password":{  
        "8888":"20181023",  
        "9001":"mimawhat"  
        },  
        "timeout":300,  
        "method":"rc4-md5",  
        "fast_open": true,  
        "workers": 2  
        }  
        ```
*   启动/停止shadowsocks
    *   `ssserver -c /etc/shadowsocks/config.json -d start`  \#可写在脚本中
    *   `ssserver -d stop`
*   优化配置
    *   `vim /etc/security/limits.conf`  
        * soft nofile 51200  
        * hard nofile 51200
    *   `ulimit -n 51200`
    *   `vim /etc/sysctl.conf`  
    *   ```
        fs.file-max = 51200  
        net.core.rmem_max = 67108864  
        net.core.wmem_max = 67108864  
        net.core.netdev_max_backlog = 250000  
        net.core.somaxconn = 4096  
        net.ipv4.tcp_syncookies = 1  
        net.ipv4.tcp_tw_reuse = 1  
        net.ipv4.tcp_tw_recycle = 0  
        net.ipv4.tcp_fin_timeout = 30  
        net.ipv4.tcp_keepalive_time = 1200  
        net.ipv4.ip_local_port_range = 10000 65000  
        net.ipv4.tcp_max_syn_backlog = 8192  
        net.ipv4.tcp_max_tw_buckets = 5000  
        net.ipv4.tcp_fastopen = 3  
        net.ipv4.tcp_mem = 25600 51200 102400  
        net.ipv4.tcp_rmem = 4096 87380 67108864  
        net.ipv4.tcp_wmem = 4096 65536 67108864  
        net.ipv4.tcp_mtu_probing = 1  
        net.ipv4.tcp_congestion_control = hybla```
    *   `sysctl -p`