# OpenWRT

## 故障及解决方案

### OpenWRT 突然无法访问国内，外网正常

OpenWRT 内运行有 ShadowSocksR Plus+，能正常访问外网。
停运 ShadowSocksR Plus+ 后，也依旧无法访问内网。登录 QQ ，报防火墙相关问题信息。

**解决方法**

在 OpenWRT 中，网络 -> 防火墙 -> 自定义规则，原有规则不动，并添加如下规则：

```
iptables -t nat -I POSTROUTING -j MASQUERADE
```

重启防火墙，以生效。

现在就能正常访问国内的网站了。

（讲道理很玄学，之前啥都没动，在断电关机后重新通电开机，就突然出现这个问题）