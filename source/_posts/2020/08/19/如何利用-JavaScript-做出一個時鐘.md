---
title: 如何利用 JavaScript 做出一個時鐘
tags:
  - JavaScript
  - CSS
category: JavaScript
abbrlink: 44267
date: 2020-08-19 16:11:28
---
# 如何利用 JavaScript 做出一個時鐘
## HTML
我們要創建一個 `div`，裡面要包裹著時針、分針，秒針和 數字 1 ~ 12
```
<div class="clock">
        <div class="hand hour data-hour-hand"></div>
        <div class="hand minute data-minute-hand"></div>
        <div class="hand second data-second-hand"></div>
        <div class="number number1">1</div>
        <div class="number number2">2</div>
        <div class="number number3">3</div>
        <div class="number number4">4</div>
        <div class="number number5">5</div>
        <div class="number number6">6</div>
        <div class="number number7">7</div>
        <div class="number number8">8</div>
        <div class="number number9">9</div>
        <div class="number number10">10</div>
        <div class="number number11">11</div>
        <div class="number number12">12</div>
    </div>
```
## CSS
### 時鐘介面
我們先給背景色，在給 `.clock` 寬高和外框把它變圓形。
```
*, *::after, *::before {
    box-sizing: border-box;
    }
body{
    background-color: #D9AFD9; //設置背景色
}
// 時鐘
.clock{
    width: 300px; //寬
    height: 300px; //高
    background-color: rgba(255,255,255,.8); //時鐘的背景色
    border-radius: 50%; //變圓
    border: 2px solid black; //給個外框
}
```
### 時鐘數字
利用絕對定位，把數字定位在時鐘上，所以先給`.clock` ，`position:relative;`
設置`--rotation`變數，一個圓為 360°，時鐘為 12 小時制，所以`360°/12=30°`，
每前進一格為30度，再把個角度帶入變數中。

```
// 時鐘
.clock{
    width: 300px;
    height: 300px;
    background-color: rgba(255,255,255,.8);
    border-radius: 50%;
    border: 2px solid black;
    position: relative; // 要定位在時鐘上
}
// 時鐘數字
.clock .number{
    --rotation:0; //設置變數，起始為 0 度
    position: absolute;
    width: 100%;
    height: 100%;
    text-align: center; 
    transform: rotate(var(--rotation));
    font-size: 1.5rem;
}
// 帶入角度
// 360deg/12=30deg
.clock .number1{--rotation:30deg;}
.clock .number2{--rotation:60deg;}
.clock .number3{--rotation:90deg;}
.clock .number4{--rotation:120deg;}
.clock .number5{--rotation:150deg;}
.clock .number6{--rotation:180deg;}
.clock .number7{--rotation:210deg;}
.clock .number8{--rotation:240deg;}
.clock .number9{--rotation:270deg;}
.clock .number10{--rotation:300deg;}
.clock .number11{--rotation:330deg;}

```
### 時針、分針、秒針
先設定共通 `.hand`，因為我們有設 `left:50%`，所以要下個`transform: translateX(-50%)`使它置中，再利用`transform-origin:bottom`，把中心點定成下方。

時針、分針、秒針 再給予寬高、背景色。
```
//共通

.clock .hand{
    --rotation:0;
    position: absolute;
    left: 50%;
    bottom: 50%;
    background-color: black;
    border: 1px solid white;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    z-index: 10; //保證在最上面
    transform-origin: bottom; // 中心點定在下方
    // 使它置中 和帶入函數及變數
    transform: translateX(-50%) rotate(calc(var(--rotation)*1deg)); 
}

// 秒針
.clock .hand.second {
    width: 3px;
    height: 45%;
    background-color: red;
}
// 分針
.clock .hand.minute {
width: 7px;
height: 40%;    
background-color: black;
}
// 時針
.clock .hand.hour {
width: 10px;
height: 35%;
background-color: black;
}
```
### 中心點
我們利用偽元素製作出一個中心圓，並利用`transform: translate(-50%, -50%);`使它置中。
```
.clock::after {
    content: '';
    position: absolute;
    background-color: black;
    z-index: 11; //要使它在最上面
    width: 15px;
    height: 15px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%); //置中
    border-radius: 50%;
}
```
### 時鐘置中
我們要使時鐘在瀏覽器置中，利用 `flex` 並給予高度，避免卷軸滾動，
在加入`overflow:hidden;`
```
body{
    background-color: #D9AFD9;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh; //給予高度
    overflow: hidden; //避免卷軸滾動
}
```
## JavaScript
我們利用`setInterval`達到每秒更新，在創建一個`setClock`函數算份數，
分數要再加入當前的秒數。ex:12分12秒為 0.22份，
時數要再加入當前的分數，但時鐘為 12 小時一圈，故除以12，
在帶入`setRotation`函數，計算角度並把角度值加入到 css 中。
```
const hourHand=document.querySelector('.data-hour-hand');
const minuteHand=document.querySelector('.data-minute-hand');
const secondHand=document.querySelector('.data-second-hand');
setInterval(setClock,1000);

function setClock(params) {
    const currentDate=new Date();
    const secondsRatio= currentDate.getSeconds()/60
    // 分數要再加入當前的秒數。ex:12分12秒為 0.22份
    const minutesRatio= (secondsRatio+currentDate.getMinutes())/60
    // 時數要再加入當前的分數，但時鐘為 12 小時一圈，故除以12
    const hourRatio= (minutesRatio+currentDate.getHours())/12
    setRotation(secondHand,secondsRatio)
    setRotation(minuteHand,minutesRatio)
    setRotation(hourHand,hourRatio)
}
// 角度
function setRotation(element,rotationRatio) {
    element.style.setProperty('--rotation',rotationRatio*360)
}
```
<p class="codepen" data-height="400" data-theme-id="light" data-default-tab="css,result" data-user="jasonuse" data-slug-hash="abNmpdO" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="JavaScript Clock">
  <span>See the Pen <a href="https://codepen.io/jasonuse/pen/abNmpdO">
  JavaScript Clock</a> by 曾慶榮 (<a href="https://codepen.io/jasonuse">@jasonuse</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## 參考資料
https://www.youtube.com/watch?v=Ki0XXrlKlHY
https://ithelp.ithome.com.tw/articles/10136005

