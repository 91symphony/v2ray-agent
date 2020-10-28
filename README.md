# v2ray-agent

- 推荐 [一键CDN+TLS+WebSocket+Nginx+V2Ray（Vmess/VLESS）+伪装博客脚本【小白推荐】](#全自动websockettlscdn智能优选cloudflare-ip一键脚本)
- 此项目采用[CDN+TLS+Nginx+V2Ray（Vmess/VLESS）](#全自动websockettlscdn智能优选cloudflare-ip一键脚本)、[Trojan](#2Trojan)、[Cloudflare Workers](#方法3workers) 进行模拟正常网站并突破防火墙，同时包含优化方法，以及简单的原理讲解。
- [优化方案【CDN自选IP、断流优化】](https://github.com/mack-a/v2ray-agent/blob/master_backup/optimize_V2Ray.md)
- [流量中转教程 wikihost](https://github.com/mack-a/v2ray-agent/blob/master_backup/traffic_relay.md)
- [自建教程](#自建教程)可以快速入手并知晓其中的步骤。如遇到不懂以及不理解的可以加入[TG群讨论](https://t.me/technologyshare)。
- [免费订阅链接【240.93 GB of 2 TB Used 2020-9-6】](https://github.com/mack-a/v2ray-agent/blob/master_backup/free_account.md)。
- [建议安装脚本前先安装适合自己的BBR](https://github.com/mack-a/v2ray-agent/blob/master_backup/bbr.md)
- 以上有问题可以提issues、加入[TG群](https://t.me/technologyshare)、[订阅频道](https://t.me/v2rayagentshare)。
- [博客地址](https://blog.v2ray-agent.com/)

* * *
# 目录
- [一键脚本](#一键脚本)
  * [1.WebSocket+TLS+CDN+智能优选Cloudflare IP](#全自动websockettlscdn智能优选cloudflare-ip一键脚本)
- [自建教程](#自建教程)
  * [1.V2Ray](#1v2ray)
  * [2.Trojan](#2trojan)
- [流量转发服务](#流量转发服务)
   * [1.TLS+WS](#1tlsws点击查看)
   * [2.TCP+Vmess](#2tcpvmess点击查看)
* * *
# 一键脚本
## 全自动WebSocket+TLS+CDN+智能优选Cloudflare IP一键脚本
- 目前已在GCP上测试Centos[6【不稳定】、7、8]、Debian[9、10]、Ubuntu[16、18、19、20]通过，不开启Cloudflare的云朵则为直连。
- 这里添加了默认的智能解析自选CDN IP，脚本安装时可手动选择是否使用，本地dns解析建议使用 [114.114.114.114]
- 如果智能解析后发现不能上网，第一可以升级客户端、第二可以将address填写自己的科学上网的域名，不再使用智能解析CDN的域名，~~Shadowrocket可以将伪装域名添加到外层的Peer【Shadowrocket不兼容所致，请升级客户端】~~。
- 如果对默认的不满意，则可以[自己进行测试](https://github.com/mack-a/v2ray-agent/blob/master_backup/optimize_V2Ray.md#1%E6%89%8B%E5%8A%A8%E8%87%AA%E9%80%89ip%E5%BB%BA%E8%AE%AE%E4%BD%BF%E7%94%A8%E8%AF%A5%E7%A7%8D%E6%96%B9%E6%B3%95)，寻找适合自己的CDN IP。
- [脚本更新日志](https://github.com/mack-a/v2ray-agent/releases)


# 示例图
- 未安装
<img src="https://raw.githubusercontent.com/mack-a/v2ray-agent/master_backup/fodder/install/一键脚本未安装.png" width=400>

- 已安装
<img src="https://raw.githubusercontent.com/mack-a/v2ray-agent/master_backup/fodder/install/一键脚本已安装01.png" width=400>
<img src="https://raw.githubusercontent.com/mack-a/v2ray-agent/master_backup/fodder/install/一键脚本已安装02.png" width=400>


## 尝鲜版脚本
- 脚本示例图
<img src="https://raw.githubusercontent.com/mack-a/v2ray-agent/dev/fodder/install/install_尝鲜版_01.png" width=400>
<img src="https://raw.githubusercontent.com/mack-a/v2ray-agent/dev/fodder/install/install_尝鲜版_02.png" width=400>

- V2Ray+VLESS+TLS+TCP+Web/V2Ray+Vmess+TLS+WS+Web[CDN 云朵必须为灰色]
- 适合线路较好或者线路中专，[中专教程](https://github.com/mack-a/v2ray-agent/blob/master_backup/traffic_relay.md)

```
bash <(curl -L -s https://raw.githubusercontent.com/mack-a/v2ray-agent/dev/install.sh)
```

# 自建教程
# 1.V2Ray
- ios端建议使用Quantumult，表现要比Trojan好。

## 方法1(Flexible)【建议使用该方法】
- 只使用CloudFlare的证书
- 客户端->CloudFlare使用TLS+vmess加密，CloudFlare->VPS只使用vmess，[点击查看](https://github.com/mack-a/v2ray-agent/blob/master_backup/Cloudflare_Flexible.md)
- 不需要自己维护自己的https证书
- 少一步解析证书的过程，速度理论上会快一点

## 方法2(Full)
- 需要自己生成https证书，并自己维护，一般使用let's encrypt生成有效期为三个月。
- 客户端->CloudFlare使用CLoudFlare TLS+vmess加密，CloudFlare->VPS使用let's encrypt TLS+vmess加密，[点击查看](https://github.com/mack-a/v2ray-agent/blob/master_backup/Cloudflare_Full.md)
- 与方法1不同的是，CloudFlare和VPS通讯时也会使用TLS加密。两个方法安全方面区别不是很大。

## 方法3(Workers)
- [点击查看](https://github.com/mack-a/v2ray-agent/blob/master_backup/cloudflare_workers.md)

# 2.Trojan
- 需要自己生成证书
- 客户端->使用自己生成的tls加密无其他加密->VPS,[点击查看](https://github.com/mack-a/v2ray-agent/blob/master_backup/Trojan.md)
- 少一层加密，理论速度会快一些。
- 速度取决于VPS的线路。
- 需要自己维护证书。
- [官方Github](https://github.com/trojan-gfw/trojan)
