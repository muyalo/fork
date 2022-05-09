# Heroku-vless

再次声明，免费服务，且用且珍惜，尽量不要滥用。

## 简介
Heroku是一个支持多种编程语言的云平台即服务。目前支持Ruby、Java、Node.js、Scala、Clojure、Python、PHP和Perl等语言，基础操作系统是Debian。

本项目用于在 Heroku 上部署 vless+websocket+tls，每次部署自动选择最新的 alpine linux 和 xray core。相比vmess，vless的性能更加优秀，占用资源更少，运行更加稳定。

建议使用cloudflare的workers的流量中转，速度更快，原则上使用后不会有被墙风险。

## 一键部署

经测试本镜像占用内存资源较低，运行稳定。点击下方紫色图标部署。

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https%3A%2F%2Fgithub.com%2Frptec%2Fheroku-vless)


#### 注：失效问题
上方一键部署已失效，刚看到有朋友说heroku检测到代码违反服务协议，估计使用的人太多或被人举报仓库被heroku封了。

#### 解决方法：
a.这里建议你fork本代码后，在github里设置为私有，然后绑定你github到heroku部署使用，推荐这个。

b.或者也可以fork代码后，修改下面链接rptec为你自己账户名，通过链接部署。

https://dashboard.heroku.com/new?template=https://github.com/rptec/heroku-vless.git

免费服务，且用且珍惜。

## 设置

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
         url.hostname="HEROKU地址，例如 rptec.herokuapp.com";
         let request=new Request(url,event.request);
         event. respondWith(
           fetch(request)
         )
      }
    ) 
```


VLESS演示链接
自行修改其中 自选IP和你的heroku地址。不再提供演示，发现我提供了，就全用我的演示地址了，一天就能几百万连接，给账号都干趴下，自建很简单。
```
vless://10974d1a-cbd6-4b6f-db1d-38d78b3fb109@你的自选ip:443?encryption=none&flow=xtls-rprx-direct&security=tls&sni=你的HEROKU地址或CF反代地址&type=ws&host=你的HEROKU地址或CF反代地址#heroku

```
详细教程
https://92km.net/archives/VLESS-Heroku-cloudflareworkers.html

搭建中有任何问题，也可以联系我 https://t.me/herokuvless

## 云服务器自行搭建

手动搭建可参考我代码中 configure.sh内容，修改uuid等信息就可以手动部署。

建议新手使用x-ui一键安装，附带web面板。使用起来简单。

https://github.com/vaxilu/x-ui

## 测速
heroku服务器选美国区的话一般在亚马逊弗吉尼亚阿什本节点，套cf后，速度取决于你自选ip的速度。

自选IP后youtube非高峰期一般能跑30000-50000kbps。可以流畅播放4K视频。
![speedtest](https://img.21t.co/2022/04/19/8a697d.png)
原版、套CF、自选IP速度对比，自选IP明显要高出一大截。我这边在国内用手机测速speedtest一般可以跑150M以上。

## 自选IP教程
最近经常有人问如何自选ip，以前博客发过，后来因为觉得没什么作用，太简单就删了。现在重新贴出来吧，你下载下面工具自己执行即可。如果不想自己选的话，也可以使用我提供的ip.2024.ml

https://github.com/badafans/better-cloudflare-ip

![自选IP配置](https://so.21t.co/2021/06/15/ed87c8.png)

自选ip后，将图中Address中原地址修改为你自选ip（使用域名也可）。

## 临时替代品 2046 
或者你也可以 使用 https://2046.gq/ 
原域名2024.ml，2024.ga，2017.ga被墙，请更换2046.gq继续使用
使用永久优惠码 `FREE2024` 选择免费套餐，流量超出后可再次使用增加流量（注:我提供多个节点免费使用，每帐号每月1T流量，已关闭支付接口，请勿支付，其中带广告屏蔽线路，屏蔽youtube等视频站点广告，带netflix等线路支持新加坡netflix解锁）

关于2024站点，看到一直有朋友们找我问怎么支付，再次说明一下，这个免费服务使用的是我闲置的服务器，不需要付费，支付时使用优惠码 FREE2024 即可，之前默认1T流量/月，发现经常有人滥用，现在修改为100G，如果流量超出，你可以再次使用优惠码。这个我会免费下去，直到这些节点被墙。
免费服务且用且珍惜，我一直没封BT等，建议尽量别滥用，之前就有用户用来发垃圾邮件，导致被vultr停机，目前大多节点我并没限速，仅部分流量费用较贵的节点我限速50M。如果不能满足建议使用heroku或者买云服务器自行搭建。


#### 2024邀请码 

你可以找老用户索取邀请码
也可以访问 https://21t.co/admin 或https://t.me/herokuvless  获取


### 详细文字教程（面向0基础新手）感谢@我的未来不是梦 编写。
http://yun.21t.co/aliyun/电子资料/Heroku搭建教程.docx
