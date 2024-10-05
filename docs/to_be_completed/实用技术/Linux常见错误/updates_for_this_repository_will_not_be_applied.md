# Updates for this repository will not be applied

## 示例环境

- Ubuntu Server 20.04 LTS

## 报错信息

```bash
username@localhost:~$ sudo apt update
Hit:1 https://mirrors.tuna.tsinghua.edu.cn/ubuntu jammy InRelease
Get:2 https://mirrors.tuna.tsinghua.edu.cn/ubuntu jammy-updates InRelease [114 kB]
Get:3 https://mirrors.tuna.tsinghua.edu.cn/ubuntu jammy-backports InRelease [99.8 kB]
Get:4 https://mirrors.tuna.tsinghua.edu.cn/ubuntu jammy-security InRelease [110 kB]
Reading package lists... Done
E: Release file for https://mirrors.tuna.tsinghua.edu.cn/ubuntu/dists/jammy-updates/InRelease is not valid yet (invalid for another 13h 41min 22s). Updates for this repository will not be applied.
E: Release file for https://mirrors.tuna.tsinghua.edu.cn/ubuntu/dists/jammy-backports/InRelease is not valid yet (invalid for another 13h 41min 48s). Updates for this repository will not be applied.
E: Release file for https://mirrors.tuna.tsinghua.edu.cn/ubuntu/dists/jammy-security/InRelease is not valid yet (invalid for another 13h 41min 10s). Updates for this repository will not be applied.
```

## 解决方式

### 问题排查

1. 检查系统时间/时区是否正确；
2. ntpd 等服务是否正常运行；

此问题可能出现在**最小化安装**的版本上，在此版本你需要手动安装所需要的一切外部服务及软件。

### NTP 网络时间协议简介

> NTP (网络时间协议, network time protocol) 是网络中保持时间同步的协议 ([How does it work](http://www.ntp.org/ntpfaq/NTP-s-algo.htm))。简单来说，客户端通过向服务器发送带有时间戳的数据包和服务器回复带有时间戳的数据包，来获得客户端发送时间，服务端接收时间、服务端发送时间、客户端接收时间 4 个时间戳。客户端系统时间偏移量定义为 δ = (t₃ - t₀) - (t₂ - t₁)。如果运行 ntpd 服务，一般来说 ntpd 会逐渐调整时钟，避免时间跳变。这对于运行计费系统、交易系统或者其他对时间准确性和事件先后顺序敏感的操作十分重要。

### 安装 NTP 服务

```bash
# 安装 NTP 以同步系统时间，期间会提示需要重启多项服务，全部选择即可
sudo apt install ntp

# 设置 NTP 服务器，也可使用默认设置，跳过该步骤。
# 详细参阅https://tuna.moe/help/ntp/
sudo vim /etc/ntp.conf
    + server ntp.tuna.tsinghua.edu.cn
```

## 最终结果

```bash
username@localhost:~$ sudo apt update
[sudo] password for ahost:
Hit:1 https://mirrors.tuna.tsinghua.edu.cn/ubuntu jammy InRelease
Get:2 https://mirrors.tuna.tsinghua.edu.cn/ubuntu jammy-updates InRelease [114 kB]
Get:3 https://mirrors.tuna.tsinghua.edu.cn/ubuntu jammy-backports InRelease [99.8 kB]
Get:4 https://mirrors.tuna.tsinghua.edu.cn/ubuntu jammy-security InRelease [110 kB]
Get:5 https://mirrors.tuna.tsinghua.edu.cn/ubuntu jammy-updates/main amd64 Packages [573 kB]
Get:6 https://mirrors.tuna.tsinghua.edu.cn/ubuntu jammy-updates/universe amd64 Packages [417 kB]
Get:7 https://mirrors.tuna.tsinghua.edu.cn/ubuntu jammy-updates/multiverse amd64 Packages [7256 B]
Fetched 1321 kB in 2s (751 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
16 packages can be upgraded. Run 'apt list --upgradable' to see them.
```

## 参考文献

[Ubuntu 安装 NTP 服务](https://segmentfault.com/a/1190000040244977)
