---
title: Tamper使用介紹
catalog: true
date: 2017-07-23 18:37:55
subtitle: 使用工具竄改HTTP Request
header-img: "Demo.png"
tags:
- 資訊安全
categories:
- 資訊安全
---

# Tamper
&emsp;&emsp;Tamper是一款Google Chrome的plugin，能夠讓你檢視或修改HTTP/HTTPS Request Header，Firefox也有類似的add-ons [Tamper Data](https://addons.mozilla.org/zh-tw/firefox/addon/tamper-data/)，目前還沒有使用過。
![tamper_demo](tamper_screenshot_01.png)

## 連結
[Tamper Chrome Extension](https://chrome.google.com/webstore/detail/tamper-chrome-extension/hifhgpdkfodlpnlmlnmhchnkepplebkb) : 先安裝Tamper Extension，安裝好後可以在開發人員工具(F12)中看到Tamper分頁
![tamper_extension](tamper_extension_01.png)
[Tamper Chrome Application](https://chrome.google.com/webstore/detail/tamper-chrome-application/odldmflbckacdofpepkdkmkccgdfaemb) : 後安裝Tamper Application，安裝好後在Chrome的應用程式頁面中開啟
[Tamper Github](https://github.com/google/tamperchrome) : 內有詳細的圖文使用教學

## 使用
&emsp;&emsp;Tamper的介面一目了然，在開發人員工具頁面中將Request Headers勾選後連上網站，主程式就會跳出並顯示攔下的請求資訊，此時若不按下 "OK" 網站就會一直顯示 "正在等待Tamper Chrome (extension) 擴充功能... 而卡在目前的請求發送" ，也可以勾選主程式右下角的 "ignore requests" 就不需要一直按確認而快速的記下所有的請求資訊。也可以針對特定類型的request攔下
![tamper use](tamper_use_01.png)
&emsp;&emsp;而要竄改request的話則是勾選 "Block / Reroute Requests"，主程式會跳出攔截到的請求資訊，此時修改框框裡的內容按下 "Allow" 就能修改發出的請求，在使用時同樣也可以先勾選 "ignore requests" 直到需要修改前取消勾選然後開始竄改你的請求
![tamper use](tamper_use_02.png)
題外話 : 利用這招在Facebook Messenger中的小遊戲明明只拿了低分卻也可以向朋友炫耀高分哦～