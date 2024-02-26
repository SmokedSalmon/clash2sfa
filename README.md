# Clash to sing-box Subscription Conversion Service
> Based on [xmdhs' clash2sfa](https://github.com/xmdhs/clash2sfa), here's its [original README.md](#clash2sfa)

## Modification
- degrade go version to 1.21 in [go.mod](go.mod) as currently being deploy to **Koyeb** whose buildpack toolchain does NOT support go 1.22
- Customized config template

## Deploy
### Build from Source
Once source changed, deploy is triggerred. Convenient but takes a couple minutes
#### Koyeb
Add an App ->  
Deployment method choose `Github` ->  
Use my repo: https://github.com/SmokedSalmon/clash2sfa, `master` branch ->  
Extend `Advanced`, in the `Exposing your service` section, use `8080` as exposed port ->    
> Port should be aligned with source and Docker setting. You can change this if you has grasped the whole App and be able to customize it)

Click **Apply** and deploy. Once ready, open the application url to use

#### Cloudflare Worker
> Personal favor

To be provided

#### Others
To be provided  
Platform provider list: [Server Deployment](https://metatube-community.github.io/wiki/server-deployment)

### Docker
App Image(source, toolchain, runtime...) -> deployment. Consistent on all platform, quick to deploy but cannot be triggerred by code change
You can use xmdhs' docker image - [ghcr.io/xmdhs/clash2sfa](ghcr.io/xmdhs/clash2sfa)  
Detail to be provided

## Config Template
Check [config.json.template](config.json.template) & [config-1.8+.json.template](config-1.8+.json.template)  
Detail to be provided

<br />
<br />

↓ Original `README.md` ↓

---
# clash2sfa
用于将 Clash.Meta 格式的订阅链接转换为 sing-box 格式，可用于安卓版本的 [SFA](https://sing-box.sagernet.org/installation/clients/sfa/)，ios 版本未测试。

## 部署
环境变量 `port` 控制程序运行所在的端口，若未设置默认开放在 8080 端口。

## docker
```
docker volume create clash2sfa    
docker run -d -p 8080:8080 -v clash2sfa:/server/db ghcr.io/xmdhs/clash2sfa
```
## 使用
启动后使用浏览器访问 http://ip:port

SFA remote 中填入链接，可以通过 https://yacd.metacubex.one/ 切换节点和全局/分流模式等。

demo https://clash2sfa-xmdhs.koyeb.app/ （因为转换格式需要把订阅链接发送到服务器并保存在数据库中，且数据库会**不定时删除**，建议自己部署。不过若使用参数**保存在链接中**则不会储存到数据库中，也不会因为数据库删除导致配置信息丢失。）
## 配置文件模板
对配置文件模板中大多数修改都将被保留，在模板中的 outbounds 中增加节点也会被保留。

## 可转换的协议
见 https://github.com/xmdhs/clash2singbox#%E6%94%AF%E6%8C%81%E5%8D%8F%E8%AE%AE

## 命令行版本
https://github.com/xmdhs/clash2singbox
