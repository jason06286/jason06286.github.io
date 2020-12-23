---
title: Js筆記 XMLHttpRequest
tags: JavaScript
category: JavaScript
abbrlink: 64403
date: 2020-08-14 18:38:51
---
## XMLHttpRequest
### readyState 狀態說明
0 已經產生XMLHttpRequest,但還沒連結要撈的資料
1 用了open,但還沒把資料傳送過去
2 偵測到你有用send
3 loading
4 你撈到資料了，數據已經完全接收
### open的格式
get 讀取資料
post 傳送資料到伺服器
true 同步
false 非同步
### onload
確定有資料回傳了，可使用onload來取得回傳的值
#### get
```
let xhr = new XMLHttpRequest();
// readyState 狀態
// 0  已經產生XMLHttpRequest,但還沒連結要撈的資料
// 1  用了open,但還沒把資料傳送過去
// 2  偵測到你有用send
// 3  loading
// 4  你撈到資料了，數據已經完全接收

// open('格式(get:讀取資料)','要讀取的網址',true(同步)false(非同步))
xhr.open('get','https://hexschool.github.io/ajaxHomework/data.json',true);

// true 非同步， (多數使用true)
// false 同步

// 只要讀取資料的話，填null空值即可
xhr.send(null);

console.log(xhr.responseText);

// onload 當資料確定有回傳了，則開始執行以下function
xhr.onload = function() {
  console.log(xhr.responseText);
  let data = JSON.parse(xhr.responseText);
  console.log(data);
}
```
### post
```
 let xhr=new XMLHttpRequest();
    xhr.open('post','https://hexschool-tutorial.herokuapp.com/api/signup',true);

    //傳送的格式
    xhr.setRequestHeader("Content-type","application/json")
    //xhr.setRequestHeader("Content-type","application/www-form-urlencoded")
    
    xhr.send('email=abcde@gmail.com&password=1234');
```
[Post example](https://codepen.io/jasonuse/pen/MWwvEWP)

