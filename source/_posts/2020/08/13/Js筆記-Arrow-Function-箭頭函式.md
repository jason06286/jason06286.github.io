---
title: JS 筆記 Arrow Function 箭頭函式
tags: JavaScript
category: JavaScript
abbrlink: 34258
date: 2020-08-13 15:11:07
---
![](/images/js01/js5.png)
## 箭頭函式（Arrow Function）
ES6 增加了箭頭函式使我們的程式碼更簡潔
> 去掉 `function` 加入 `=>`
> 只有一個參數 `（）`可加可不加，兩個以上一定要加 `（params,params2）`
> 箭頭函式 `this` 指向外層
### 函式比較
```
// ES5
const numbers =[2,3,4];

const double =numbers.map(function(number){
    return number * number;
});
console.log(double)
```
```
// ES6
const numbers =[2,3,4];

const double =numbers.map((number)=>{
    return number * number;
});

const double =numbers.map(number=>{
    return number * number;
});

const double =numbers.map(number=>number * number);

console.log(double)
```
### this比較
```
// ES5
const Jason={
    name:'Jason',
    hobbies:['Coding', 'Running', 'Sleeping'],
    printHobbies: function(){
        let self=this //透過宣告變數來取得外層this
        this.hobbies.map(function (hobby) {
            console.log(this) //指向window
            console.log(`${self.name} loves ${hobby}`); 
        })
    }
}
Jason.printHobbies();
```
```
// ES6
const Jason={
    name:'Jason',
    hobbies:['Coding', 'Running', 'Sleeping'],
    printHobbies: function(){
        this.hobbies.map(hobby=> {
            console.log(`${this.name} loves ${hobby}`); 
        })
    }
}
Jason.printHobbies();
```
