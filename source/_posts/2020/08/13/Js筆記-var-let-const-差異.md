---
title: JS 筆記 var let const 差異
tags: JavaScript
category: JavaScript
abbrlink: 54502
date: 2020-08-13 12:50:02
---
![](/images/js01/js1.jpg)
在 ES6 之前 JavaScript 沒有區塊域的概念，因此經常使用 `var` 來宣告變數，
而造成區域變數覆蓋到全域變數，因此才有 `let`、`const` 來避免此狀況產生。
## let 
用法就跟 `var` 沒有差別，但作用域只在括號內，讓我們看個經典例子來瞭解
```
for (var i = 0; i < 3; i++) {
  console.log(i);
  setTimeout(function () {
    console.log('這執行第' + i + '次');
  }, 10);
}
```
![](/images/js01/js2.png)
我們會發現出來的結果是 `這執行第3次`，而不是我們要的結果，
因為 `var` 宣告 `i` 會變成全域變數，造成 `for` 迴圈累加，
在 `setTimeout` 實際執行時只會拿到 3 這個數字。
此時在查找 `i`，發現 `i＝3`，疑～🧐 不是只會作用在函式裡嗎？
怎麼 window 也讀得到？
### 用 `let` 改寫
```
for (let i = 0; i < 10; i++) {
  console.log(i);
  setTimeout(function () {
    console.log('這執行第' + i + '次');
  }, 10);
}
```
![](/images/js01/js3.png)
我們會發現結果會依序跑出，且查找`i`，
顯示 `Uncaught ReferenceError: i is not defined`，
`i` 變數未被宣告，因為 `let` 作用域只在括號內。
## const
是宣吿一個常數，且必須一定要有值，不可被更改。
```
const a=1;
let  a=2;
a=2
```
![](/images/js01/js4.png)
### 物件是例外
因為物件是傳址而不是傳值
```
const CLOTHES ={
    color:'red',
    size:'L',
}
CLOTHES .material="棉"
```
> 盡量少用 `var` 用 `let`、`const` 做取代
> `const` 可以宣告不太會更動的內容。ex: DOM 、物件、api
> `const` 常數可以用大寫，以利區分


