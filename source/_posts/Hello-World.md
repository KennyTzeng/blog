---
title: "Hello World"
catalog: true
date: 2017-07-10 18:47:53
subtitle: "我的部落格終於上架啦！"
header-img: "Demo.png"
tags:
- Life
categories:
- Life
---

# 緣由
&emsp;&emsp;一直很想要架一個部落格來寫文章，先前曾研究把WordPress架在Heroku上跑，資料庫的部份有人說WordPress不支援Postgres因此改用Heroku上另一個add-ons clearDB，成功是成功了不過我安裝的套件每次在網站30分鐘閒置後重啟就會消失，最後以失敗告終(哭)。
&emsp;&emsp;好家在最近看到了[Hexo](https://hexo.io/zh-tw/)這套可以幫我們產生靜態頁面的框架，而且還支援超好用的MarkDown標記語言，主題我選用了[Hux](http://huangxuan.me/)大大(re-ported by [BeanTech](http://beantech.org/))所開源的專案，頁面的設計還得再研究研究，總之先把部落格給放上來啦～功用是**紀錄自我學習歷程，希望能幫助到正在學習的他人**(雖然說我還很廢 嗚嗚)。

# Hexo使用
[Hexo官網](https://hexo.io/zh-tw/index.html) 需要先安裝好NodeJS
安裝指令
```
npm install hexo-cli -g
```

---
第一次打文章不知道md要怎麼表示段落首行開頭的空格，上網查了發現全行空格可以使用`&emsp;`因此用兩個即可。