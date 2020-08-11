---
title: 從零開始，如何從 Git push 到 GitHub？
tags: git
category: git
abbrlink: 38287
date: 2020-08-11 14:32:06
---

本篇適用於完全不會`Git`的人，將一步步帶你上傳檔案至`GitHub`
## 安裝
首先到 [ Git 官網](https://git-scm.com/) ，下載`Git`
以下為` windows` 環境下示範 ，開始選單> 所有程式> `Git`> `Git Bash`
然後開啟` Git Bash`
![](/images/git01/git1.png)

### 讓我們瞭解基本的 `command` 指令
1. 移動路徑：cd 路徑
2. 回上一層：cd .. 
3. 開新資料夾： mkdir 資料夾名稱
4. 開新檔案： touch 檔案名稱
### 設定
首先先設定使用者的資料，這些資訊將作為提交者資訊顯示在版本控制的歷史記錄中。
```
$ git config --global user.name "<使用者名字>"
$ git config --global user.email "<電子信箱>"
$ git config --list //來確認使用者資料
```
![](/images/git01/git2.png)
## Git 基礎操作
### 創建 Git 
```
新增一個資料夾
cd 資料夾的路經 
$ git init //開啟一個新的 git 
$ touch index.html //建立一個檔案,可依自己需求建立，此示範為 index.html
```
![](/images/git01/git3.png)
### 確認工作目錄與索引的狀態
從下圖我們得知檔案還未 `commit` , 系統建議我們先把它加入索引,不然會 `commit `不到
```
$ git status 
```
![](/images/git01/git4.png)
### 將檔案加入至索引
透過 `$ git status`，我們得知檔案已被加入索引。
```
$ git add '檔案名稱' //加入指定檔案
$ git add . //未加入的檔案一次加入
$ git status
```
![](/images/git01/git5.png)
### 執行`commit`命令提交檔案
最後只要執行 `git commit -m "更新註解"` 就可以將本次更新的內容提交到數據庫了。
```
$ git commit -m "update1" 
$ git log //查詢提交記錄
```
![](/images/git01/git6.png)
## 遠端數據庫 GitHub
### 申請 [GitHub](https://github.com/) 帳號
申請完 `GitHub` 帳號，我們要創建一個資料夾，來當遠端數據庫。
![](/images/git01/git7.png)
![](/images/git01/git8.png)
![](/images/git01/git9.png)

### 連結至 GitHub 遠端數據庫
透過 `$ git clone 'GitHub 的 URL'`，連結至 `GitHub` 的遠端數據庫
```
$ git clone 'GitHub 的 URL'
```
![](/images/git01/git9.5.png)
### 上傳至 GitHub 專案
透過 `$ git push `將本地端數據庫上傳至雲端數據庫 ，會要求你輸入 `GitHub` 的帳號密碼以確認。
```
$ git push
```
![](/images/git01/git10.png)
![](/images/git01/git11.png)
![](/images/git01/git12.png)
> 操作過一次流程，我們就瞭解
> `$ git init` 建立工作目錄 
> `$ git add .` 把工作目錄的檔案加入索引
>` $ git commit -m ''` 將索引的檔案提交至本地數據庫
>  `$ git clone 'URL'` 連接至遠端數據庫
>  `$ git push`  本地端數據庫上傳至雲端數據庫

![](/images/git01/git13.png)
