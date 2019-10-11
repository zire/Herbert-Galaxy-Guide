# How To Set Up Shadowsocks

## Select VM Vendor

Digital Ocean was chosen for its reputation, price $5/month in its lowest tier), and readily available [guide](https://www.vpndada.com/how-to-setup-a-shadowsocks-server-on-digitalocean/). AWS Lightsail doesn't seem to have fast enough connection and its server was relatively new compared to well established Digital Ocean. Linode might be a good choice too, but I aleady use Linode for other sites and diversification might be a good idea.

## Set Up VM

Choose an image: `Distributions/Ubuntu/18.04.3 (LTS)`

Choose a plan: `Starter/Standard/$5`, which has the following set of parameters:

- $5/month
- $0.007/hour
- 1 GB / 1 CPU
- 25 GB SSD dick
- 1,000 GB transfer

Add block storage: `none`

Choose a datacenter region: `San Francisco/2`

Select additional options: `none`

Authentication: `SSH keys`

Then proceed to create the droplet. 

## Configure Shadowsocks Server

Login as root.

Update the machine:

```
$ apt-get update
```

Install shadowsocks:

```
$ apt-get install python-pip
$ pip install shadowsocks
```

For optimized performance, suggest to use `chacha20` encryption method. Install this encryption with the following command:

```
$ apt-get install python-m2crypto
$ apt-get install build-essential
$ wget https://github.com/jedisct1/libsodium/releases/download/1.0.10/libsodium-1.0.10.tar.gz
$ tar xf libsodium-1.0.10.tar.gz && cd libsodium-1.0.10
$ ./configure && make && make install
$ ldconfig
```

Create a configuration file for Shadowsocks

```
$ vim /etc/shadowsocks.json
```

Add the following content to the shadowsocks config file

```
{
    "server":"your_droplet's_IP_address",
    "server_port":8000,
    "local_port":1080,
    "password":"your_password",
    "timeout":600,
    "method":"chacha20"
}
```

The above supports one port on the shadowsocks server and one login. To support multiple users each with different passwords, we can set up multiple ports:

```
{
    "server":"your_droplet's_IP_address",
    "port_password": {
        "443": "password1",
        "8000": "password2",
        "8383": "password3",
        "8384": "password4"
    },
    "local_port":1080,
    "timeout":600,
    "method":"chacha20"
}
```

Start the shadowsocks server

```
$ ssserver -c /etc/shadowsocks.json -d start
```

To check if everything is OK, take a look on Shadowsocks' log file

```
$ less /var/log/shadowsocks.log
```

If there is no error message in the log file, then the server is running fine.

To stop or restart the Shadowsocks server:

```
$ ssserver -c /etc/shadowsocks.json -d stop
$ ssserver -c /etc/shadowsocks.json -d restart
```

To make sure every time the server reboots, our Shadowsocks server will be stated automatically:

```
$ vim /etc/rc.local
```

And add this to the bottom of the file:

```
/usr/bin/python /usr/local/bin/ssserver -c /etc/shadowsocks.json -d start
```

## Optimize Shadowsocks Server

By default, Shadowsocks server might not be able to handle a lot of traffic. To handle a large amount of concurrent connections, we need to increase the maximum number of open file descriptions:

```
$ vim /etc/security/limits.conf
```

Add the following two lines to this file:

```
* soft nofile 51200
* hard nofile 51200
```

Temporarily stop the Shadowsocks server

```
$ ssserver -c /etc/shadowsocks.json -d stop
```

Set the ulimit:

```
$ ulimit -n 51200
```

Next tune some kernel paramters:

```
$ vim /etc/sysctl.conf
```

Add the following lines to the end of the file:

```
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
net.ipv4.tcp_congestion_control = cubic
```

To make these changes take effect:

```
$ sysctl -p
```

And restart the Shadowsocks server

```
$ ssserver -c /etc/shadowsocks.json -d start
```

## Configure Shadowsocks Client

Shadowsocks' official page has listed popular clients on various platforms:

![Shadowsocks client list](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/shadowsocks_clients.png)

I use this one [Shadowsocks-iOS](https://github.com/shadowsocks/shadowsocks-iOS/wiki/Shadowsocks-for-OSX-Help) and the current latest version is `ShadowsocksX-2.6.3.dmg`

Open ShadowsocksX-2.6.3 => Servers => Open Server Preferences

Enter the server IP address for the server (Digital Ocean droplet), the port number, and password as per the earlier `/etc/shadowsocks.json` config file. Pick `chacha20` as the encryption method.

Use `Global Mode` to route all traffic through Shadowsocks server. Use `Auto Proxy Mode` to route traffice according to websites listed in the PAC list. 

## Testing Tools

TCP usually has port 22, which is used by SSH. There are two protocols for ping, TCP and ICMP. It's possible that an IP can be ping-ed through ICMP protocol, but it cannot be SSH-ed because TCP has been blocked.

Ping test A to see if an IP address is blocked in China: [https://tools.ipip.net/ping.php](https://tools.ipip.net/ping.php). If there is no packet loss in US sites but close to 100% loss in China sites, then this IP is blocked.

Ping test B to see if the IP + port works from outside of China: [https://www.yougetsignal.com/tools/open-ports/](https://www.yougetsignal.com/tools/open-ports/). 

Ping test C to see if the same IP + port works from within China: [http://tool.chinaz.com/port](http://tool.chinaz.com/port)

If this IP + port is `open` in B, but `closed` in C, then pretty certainly this IP has been blocked. 

## References

[Connecting to DigitalOcean Server to Setup Shadowsocks](https://www.vpndada.com/how-to-setup-a-shadowsocks-server-on-digitalocean/)

[如何使用Linode vps来搭建自己shadowsocks服务！](https://steemit.com/vpn/@rickyshi/linode-vps-shadowsocks)

[Shadowsocks Client List](https://shadowsocks.org/en/download/clients.html)

***

[Back to HitichHikder's Guide by Herbert](README.md)