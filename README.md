# Heroku-vless

## 简介
Heroku是一个支持多种编程语言的云平台即服务。目前支持Ruby、Java、Node.js、Scala、Clojure、Python、PHP和Perl等语言，基础操作系统是Debian。

本项目用于在 Heroku 上部署 vless+websocket+tls，每次部署自动选择最新的 alpine linux 和 xray core。相比vmess，vless的性能更加优秀，占用资源更少，运行更加稳定。

刚测试了一下，herokuapp.com这个域名部分地区已经被墙（2021.9.27），故现在如果不配置cf流量中转，这个将无法稳定使用，建议使用cloudflare的workers的流量中转，速度更快，原则上使用后不会有被墙风险。

## 镜像

经测试本镜像占用内存资源较低，运行稳定。

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https%3A%2F%2Fgithub.com%2Frptec%2Fheroku-vless)

## 注意

### 路径

`WebSocket` 路径(配置文件中的 `path` )为 `/` 。你也可以自行修改

### 端口

`端口` 为 `443` 。 


### UUID

`UUID` 默认为 `10974d1a-cbd6-4b6f-db1d-38d78b3fb109` 你也可以在部署时自由修改（建议修改）。

## 流量中转

使用cloudflare的workers来`中转流量`，配置为： 

```
addEventListener(
      "fetch",event => {
         let url=new URL(event.request.url);
         url.hostname="你的heroku域名.herokuapp.com";
         let request=new Request(url,event.request);
         event. respondWith(
           fetch(request)
         )
      }
    ) 
```


详细教程
https://92km.net/archives/VLESS-Heroku-cloudflareworkers.html

搭建中有任何问题，也可以联系我 https://t.me/herokuvless


当然最后如果你还是懒得搭建的话，可以使用我搭建并提供的。
```
vless://10874d1a-cbd6-4b6f-db1d-38d78b3fb108@ip.2024.ml:443?flow=xtls-rprx-direct&encryption=none&security=tls&type=ws&host=cdn.2024.ml#heroku永久免费
```

或者你也可以 使用 https://2024.ml/ 

使用永久优惠码 `FREE2024` 选择免费套餐，流量超出后可再次使用增加流量（注:我提供多个节点免费使用，每帐号每月1T流量，已关闭支付接口，请勿支付，其中带广告屏蔽线路，屏蔽youtube等视频站点广告，带netflix等线路支持新加坡netflix解锁）

注册邀请码：

```
l3aBsKkP
VTheVHYQ
7dtHQxi6
bUsqXvuz
ls7spXgk
brBpflpF
nq3sfOrJ
vkKxIOuk
CVrcUnjY
vQwMyMvj
```

如果以上不能满足你需要（例如不同地区流媒体解锁等），你可以自己购买vps，自己搭建。
### 近期特价服务器推荐
virmach最近一直有黑五电商星期一活动，常规配置6.3刀一年 折合人民币不到40元一年，支持支付宝，paypal付款。建议选择西雅图，圣何塞，洛杉矶节点，到国内速度不错。。。同时我自己买的水牛城和圣何塞节点，测试都可以观看netflix美国地区非自制片。
https://billing.virmach.com/aff.php?aff=1179&url=www.virmach.com/special-offers

cloudcone双十二活动，
https://app.cloudcone.com/vps/70/create?token=12.12-vps-offer-1&ref=5687


