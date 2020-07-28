---
title: shadowsockets
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-28 16:35:39
password:
summary:
Shadowsocks on Ubuntu
tags:
- 科学上网
categories:
- 服务器相关
---
<div style="font-size: 22px; padding: 0 15px 0; margin-bottom: 20px;">

<div style="padding-bottom: 24px;">Shadowsocks搭建配置</div>

</div>

*   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>apt install python python-pip python-m2crypto</span></span>
*   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>安装shadowsocks</span></span>
    *   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>pip install shadowsocks</span></span>
*   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>配置文件/etc/shadowsocks/config.json</span></span>
    *   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>单用户</span></span>  
        <span class="note" style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding: 3px 0px 2px 17px; margin-left: -17px; border-left: 1px solid rgb(235, 235, 235);">{  
        "server":"ip",  
        "server_port":8888,  
        "local_address": "127.0.0.1",  
        "local_port":1080,  
        "password":"123456789",  
        "timeout":300,  
        "method":"rc4-md5",  
        "fast_open": true,  
        "workers": 1  
        }  

        ​</span>
    *   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>多用户</span></span>  
        <span class="note" style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding: 3px 0px 2px 17px; margin-left: -17px; border-left: 1px solid rgb(235, 235, 235);">{  
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
        </span>
*   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>启动/停止shadowsocks</span></span>
    *   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>ssserver -c /etc/shadowsocks/config.json -d start</span> <span>#可写在脚本中</span></span>
    *   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>ssserver -d stop</span></span>
*   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>优化配置</span></span>
    *   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>vim /etc/security/limits.conf</span></span>  
        <span class="note" style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding: 3px 0px 2px 17px; margin-left: -17px; border-left: 1px solid rgb(235, 235, 235);">* soft nofile 51200  
        * hard nofile 51200​</span>
    *   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>ulimit -n 51200</span></span>
    *   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>vim /etc/sysctl.conf</span></span>  
        <span class="note" style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding: 3px 0px 2px 17px; margin-left: -17px; border-left: 1px solid rgb(235, 235, 235);">fs.file-max = 51200  
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
        net.ipv4.tcp_congestion_control = hybla</span>
    *   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;"><span>sysctl -p</span></span>