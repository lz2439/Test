参考链接：[IP V4环境下群晖部署WireGuard服务端 和 客户端教程_网络存储_什么值得买](https://post.smzdm.com/p/awzvz6r2/)

### 一、服务端

部署环境：thinkpad、fnos、docker

docker-compose.yml:
```docker
version: '3'

services:
  wireguard:
    image: linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
    environment:
      - PUID=1000
      - PGID=1000
      - SERVERURL=zw0130.top  # 服务器的公网IP或域名
      - SERVERPORT=51820                  # WireGuard 监听的端口
      - PEERS=iphone,y7000p,synology                      # 客户端的名称
      - PEERDNS=223.5.5.5                   # DNS 设置
      - INTERNAL_SUBNET=10.252.1.0        # 内网IP段
      - ALLOWEDIPS=10.252.1.0/24,10.0.0.0/24             # 允许的 IP 地址范围
    volumes:
      - ./config:/config                  # 配置文件存放路径
    ports:
      - 51820:51820/udp                   # 映射端口
    restart: unless-stopped

```

注意点：
	需要在路由器放通51820端口，端口是udp端口
	客户端怎么加？
		在PEERS=iphone,y7000p,synology里面，每一个是一个客户端，添加好重启docker-compose即可。
	放通网段：ALLOWEDIPS=10.252.1.0/24,10.0.0.0/24
	内网ip段本身会占用.1地址：INTERNAL_SUBNET=10.252.1.0 。然后客户端是依次增加

二、客户端
	windwos
		下载客户端，导入配置即可，配置在服务端config目录下
	ios
		国外账号下载客户端，扫码即可
	群晖
		先安装wireguard套件，正常运行后，创建目录，导入配置，删除dns，然后启动，具体见前面参考链接

```python
   #群晖配置
   41  cd /etc/wireguard/    #创建目录
   42  ls
   43  cp "/volume1/homes/zhouhao/peer_synology.conf" .     #copy文件
   44  ls
   45  wg-quick up peer_synology.conf        #启动配置
   46  wg show peer_synology    #查看链接
   47  wg show peer_synology
   48  ip a    #查看网口
   49  sudo wg-autostart enable peer_synology    #设置开机自启动
   50  ping 10.0.0.253    #网络测试
   51  history
```

