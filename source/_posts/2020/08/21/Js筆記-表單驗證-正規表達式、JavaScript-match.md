---
title: 'Js筆記 表單驗證-正規表達式、JavaScript match() '
tags:
  - JavaScript
category: JavaScript
abbrlink: 17906
date: 2020-08-21 15:11:22
---

## JavaScript  match()
通常都會搭配正規表達式使用，若找到匹配的內容會回傳內容，
反之則傳回`null`.
```
let str='abc123'
// 含數字或小寫字母之字串
let re=/[a-z0-9]/
// 篩選
let found=str.match(re)
console.log(found)
```
![](/images/match/match1.png)
## 正規表達式
![](/images/match/regexp.gif)
`/要驗證的內容/`
![](/images/match/match2.png)
![](/images/match/match3.png)
![](/images/match/match4.png)
### 帳號註冊範例
```
 // 帳號驗證
    if (emailStr === '') {
        reportOfEmail.innerHTML = 'Email不能為空'
    } else if (emailStr.match(/[@]+/) === null ) {
    reportOfEmail.innerHTML = 'Email必須包含 @符號'
    } else if (emailStr.match(/[.]+/) === null ) {
    reportOfEmail.innerHTML = 'Email格式錯誤'
    } else {
    reportOfEmail.innerHTML = ''
    account.email=emailStr;
    }
    // 密碼驗證
    if (passwordStr === '') {
        reportOfPassword.innerHTML = '密碼不能為空'
    } else if (passwordStr.match(/[a-zA-Z]+/) === null || passwordStr.match(/[0-9]+/) === null) {
    reportOfPassword.innerHTML = '密碼需包含英數'
    } else {
    reportOfPassword.innerHTML = ''
    account.password=passwordStr;
    }
```
## 參考文章
https://jonas1011.pixnet.net/blog/post/26065399
https://www.runoob.com/jsref/jsref-match.html
https://5xruby.tw/posts/learn-regular-expression/
