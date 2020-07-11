# Guide on frp to visit NAS from Outside

## 1 Download frp 

Find out the the version for server

```
$ uname -a
Linux starlord 4.15.0-1045-aws #47-Ubuntu SMP Fri Aug 2 13:50:30 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```

and 

```
$ arch
x86_64
```

`aarch64` is ARM structure and `x86` is X86 structure.

Here's the [https://github.com/fatedier/frp](https://github.com/fatedier/frp). 

Find the right distro package: [https://github.com/fatedier/frp/releases](https://github.com/fatedier/frp/releases)

Guide in Chinese: [https://github.com/fatedier/frp/blob/master/README_zh.md](https://github.com/fatedier/frp/blob/master/README_zh.md)

ssh into NAS

```
$ wget https://github.com/fatedier/frp/releases/download/v0.33.0/frp_0.33.0_linux_arm64.tar.gz
```

## Configure frp on server

Unzip the compressed installation file

```
$ tar -xvf frp_0.33.0_linux_arm64.tar.gz
```

Enter into the frp folder

```
$ cd frp_0.33.0_linux_arm64/
```

Delete files related to client side

```
$ rm -f frpc frpc_full.ini frpc.ini
```

Edit `frps.ini` file. `vi frps.ini`:

```
[common]
bind_port = 7000
```

Start frp service on server

```
$ ./frps -c ./frps.ini
```

If running into `./frps: cannot execute binary file: Exec form` that means the downloaded frp version is not compatible with the server version. Need to find the right version.

```
2020/06/06 22:35:42 [I] [service.go:178] frps tcp listen on 0.0.0.0:7000
2020/06/06 22:35:42 [I] [service.go:220] http service listen on 0.0.0.0:8080
2020/06/06 22:35:42 [I] [service.go:277] Dashboard listen on 0.0.0.0:7500
2020/06/06 22:35:42 [I] [root.go:209] start frps success
```

## Configure frp on NAS

Delete server-side files

```
$ rm -f frps frps_full.ini frps.ini
```

## References

[如何用 Frp 实现外网访问群晖 NAS - 2020/03/22](https://blog.csdn.net/Arthur_Holmes/article/details/105038925)

[frps+nginx内网穿透安装与配置 - 2019/07/24](https://www.codeceo.org/server/435.html)

[FRP内网穿透访问家中的NAS和路由器后台-2019/04/21](https://blog.csdn.net/u010519914/article/details/89440136)

[利用 FRP 实现外网访问 NAS-2020/04/09](https://blog.csdn.net/u014032410/article/details/105420467)
