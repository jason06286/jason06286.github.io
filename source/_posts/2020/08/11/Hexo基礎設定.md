---
title: Hexo 基礎設定
tags: Hexo
category: Hexo
abbrlink: 17504
date: 2020-08-11 12:33:55
---
# Hexo 基礎設定
## 設定網站名稱、及作者名稱
開啟目錄資料夾中的 `_config.yml`搜尋`site`
``` npm
# Site
title: JasonCodingBlog //網站名稱
subtitle: 'Coding Road' //副標題
description: '不要等待運氣來臨，應該主動去努力掌握知識。' //網站敘述
keywords: //關鍵字
author: Jason06286 //作者名稱
language: zh-tw //語系
timezone: ''

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://jason06286.github.io/ //輸入您的網站URL
root: /
permalink: :year:month:day/:abbrlink/
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks
```
## 設定主題
下載 themes 並解壓縮到資料夾內的 themes 資料夾內，
開啟目錄資料夾中的 `_config.yml`搜尋`theme`
![](/images/hexoset/hexoset1.png)
```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: hexo-theme-next-master //更改成你所下載的主題名稱
```
## Next
### 加入 Google Analytics
這邊使用 NexT 7.8.0 模板作舉例。
進入主題 (Next) 中尋找 `_config.yml` 檔案，搜尋`Google Analytics`
```
google_analytics:
  tracking_id: 
  only_pageview: false
```
```
google_analytics:
  tracking_id: UA-XXXXXX-1 //UAID追蹤碼
  only_pageview: false
```
### 更改 Next 主題樣式
進入主題 (Next) 中尋找 `_config.yml` 檔案，搜尋`scheme`
想要使用哪一個，打開註解即可。
```
# Schemes
# scheme: Muse
# scheme: Mist
# scheme: Pisces
scheme: Gemini 
```
### 設置側邊欄
進入主題 (Next) 中尋找 `_config.yml` 檔案，搜尋`menu`，
想要使用哪一個，打開註解即可，若`tags`、`categories`跳出 404，
請參照此[解決辦法](https://www.zhihu.com/question/29017171)。
```
menu:
  home: / || fa fa-home
  # about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  # schedule: /schedule/ || fa fa-calendar
  # sitemap: /sitemap.xml || fa fa-sitemap
  #commonweal: /404/ || fa fa-heartbeat
```
### 開啟 Social Media
進入主題 (Next) 中尋找 `_config.yml` 檔案，搜尋`menu`，
想要使用哪一個，打開註解即可。
```
social:
  GitHub: https://github.com/jason06286 || fab fa-github
  E-Mail: mailto:dj4871114@gmail.com || fa fa-envelope
  #Weibo: https://weibo.com/yourname || fab fa-weibo
  #Google: https://plus.google.com/yourname || fab fa-google
  #Twitter: https://twitter.com/yourname || fab fa-twitter
  FB Page: https://www.facebook.com/profile.php?id=100000248997692 || fab fa-facebook
  #StackOverflow: https://stackoverflow.com/yourname || fab fa-stack-overflow
  #YouTube: https://youtube.com/yourname || fab fa-youtube
  #Instagram: https://instagram.com/yourname || fab fa-instagram
  #Skype: skype:yourname?call|chat || fab fa-skype
```
### 開啟 Gitalk 留言版
#### 建立 GitHub OAuth APP
由於要使用 Gitalk 必須先有 GitHub OAuth，首先開啟 GitHub → Setting
![](/images/hexoset/hexoset2.png)
接下來選擇 Developer settings
![](/images/hexoset/hexoset3.png)
然後點 OAuth Apps ，新增 New OAuth Apps
![](/images/hexoset/hexoset4.png)
接下來依照欄位填寫即可
```
Application name - 應用程式名稱
Homepage URL - 應用程式網域 → 部落格網址
Application description - 應用程式描述
Authorization callback URL - 授權回應網址 → 部落格網址
```
![](/images/hexoset/hexoset5.png)
申請完之後，你會獲得兩組 ID (Client ID、Client Secret)
![](/images/hexoset/hexoset6.png)
#### Gitalk
進入主題 (Next) 中尋找 `_config.yml` 檔案，搜尋`Gitalk`
```
gitalk:
  enable: true
  github_id:  //GitHub 作者帳號
  repo: jason06286.github.io //你的 Repo 名稱，通常就是網域
  client_id: xxxxxxxx //剛剛申請的 Client ID
  client_secret: xxxxxxxx //剛剛申請的 Client Secret
  admin_user: jason06286 //管理者的帳號
  distraction_free_mode: true //無干擾模式
  language: zh-TW //語系
```













