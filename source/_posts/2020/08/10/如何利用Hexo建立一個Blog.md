---
title: 如何利用Hexo建立一個Blog
tags: hexo
category: hexo
abbrlink: 53228
date: 2020-08-10 15:59:11
---
# 為什麼要建立 Hexo 部落格
從今年開始學習前端技術，不知不覺也過了半年了，覺得自己的技術有所成長，
可以藉由寫文章幫助大家並整合自己的技術。平台這麼多，為何我會選擇 Hexo ？

因為 Hexo 是要用指令來開發，也必須配合 Git 做使用，，是不是摸蜊仔兼洗褲呢！

 Hexo 是使用 Ｍarkdown 撰寫格式，也需要熟悉 Git 指令還有一點 npm 的知識，
 可以參考下方連結教學。

[Ｍarkdown](https://ithelp.ithome.com.tw/articles/10203758)
[Git](https://w3c.hexschool.com/git/cfdbd310)
[npm ](https://hsiangfeng.github.io/nodejs/20190626/1317979814/)
---
## 建立 Hexo 部落格
### 版本與環境

作業系統： macOs

Nodejs:：v12.18.3 LTS

IDE：VS Code
### 本文環境

#### Hexo 版本

hexo: 5.0.0

hexo-cli: 4.1.0

#### NexT 版本
Next: 7.8.0

---
## 從 GitHub 建立新的數據庫 (Creat a new Repository)
![](/images/hexoblog1.png)
* 名稱務必要謹慎設定，因為之後就無法更改，若想要修改只能重新建立數據庫，記得後面的 github.io 要打一樣的。
* 下方的權限直接用 Public (公開) 即可，若一開始還不想公開就選擇 Private (私人的)。
* 其他不用更動，直接選擇最下方的綠色按鈕 (Create repostory) 建立數據庫
![](/images/hexoblog2.png)
---
## 安裝 Hexo
使用指令安裝 Hexo，開啟終端機，輸入以下指令：

``` npm
npm install hexo-cli -g
```
指令說明：透過 npm 在 全域 (-g) 下安裝 Hexo-Cli

可以透過以下指令，確認是否安裝成功
``` npm
hexo -v
```
![](/images/hexoblog3.png)
### 建立 Hexo
在要存取的硬碟中開啟一個新資料夾，並自訂名稱 (建議用英文)，之後的資料就會在這個資料夾內，並輸入以下指令：
``` npm
hexo init projectname
```
* projectname 改成自己定義的名稱，建議用英文，安裝完成後如下圖：
![](/images/hexoblog4.png)
---
### 進入 Hexo
在終端機輸入：
``` 
cd projectname
```
* projectname 為自定義名稱
### 安裝相關套件
由於建立完畢的 Hexo 還必須安裝 npm 相關套件，所以必須在這個目錄下輸入：
``` npm
npm install
```
* 指令說明：將 package.json 相依套件下載下來

---
### 啟動 Hexo
完成上方內容後再輸入下方指令：
``` npm
hexo server
```
![](/images/hexoblog5.png)
![](/images/hexoblog6.png)
* 就會產生一個本地端 4000的網頁
## 將資料上傳至 GitHub
``` git
git init //創建一個 git 初始檔
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/jason06286/1234.git //創建一個遠端資料庫
git push -u origin master // 將資料上傳至遠端 master 分支

```
![](/images/hexoblog7.png)
### 部署 GitHub

需要安裝一個 Hexo 沒有安裝的插件
```
npm install hexo-deployer-git --save
```
修改 _config.yml 中的 Depolyment 如下：
```
deploy:
  type: git // 模式
  repo: https://github.com/yourGithub /yourGithubName.github.io.git // 自己 GitHub repos 連結
  branch: master // 分支
```
修改完後輸入下方指令：
```
hexo g d

```
* 指令說明：g →生成靜態頁面、d →部屬
## 其他指令
```
hexo new "title"
```
* 建立新文章
```
hexo s
```
* s →啟動伺服器 
```
hexo g d
```
* g →生成靜態頁面 d →部屬模式 
```
hexo clean
```
* 刪除已生成的靜態頁面及快取檔案
### 刪除指定文章
在本地端 source 資料夾，把指定的 md. 檔案刪除，在重新佈署即可，指令為：
```
hexo g d
```
---
> 參考文章：https://hsiangfeng.github.io/hexo/20190411/932826160/








