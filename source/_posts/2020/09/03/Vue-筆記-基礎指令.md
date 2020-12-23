---
title: 'Vue 筆記 基礎指令 '
tags:
  - Vue
category: Vue
abbrlink: 36391
date: 2020-09-03 14:40:04
---
## 基礎指令
### v-text v-html v-modal
> v-text == textContent
> v-html == innerHtml
> v-modal == 宣告變數 雙向
```
<div class="app">
  {{text}} //textContent
  <div v-text="text"></div> //textContent
  <div v-html="text"></div> //innerHtml
  <input type="text" v-model="text"> //雙向綁定 input.value=Vue data.text
</div>

<script>
  let app =new Vue({
    el:'.app', //綁定DOM
    data:{
      text:'<span>hello</span>'
    }
  })
</script>
```
### v-bind
可縮寫成 `:`
```
  <img :src="imgSrc"  :class="className" alt=""> //setAttribute
```
> v-bind == setAttribute
```
<div id="app">
  <img v-bind:src="imgSrc"  v-bind:class="className" alt=""> //setAttribute
</div>

<script>
var app = new Vue({
  el: '#app',
  data: {
    imgSrc: 'https://images.unsplash.com/photo-1479568933336-ea01829af8de?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=d9926ef56492b20aea8508ed32ec6030&auto=format&fit=crop&w=2250&q=80',
    className: 'img-fluid'
  }
})
</script>
```
### v-for v-if
> pre 類似console.log()，但直接渲染在網頁上。
> v-for == forEach
> v-if == if
```
<div id="app">
<pre>
  {{list}}
</pre>

<ul>
  <li v-for="(item, index) in list" v-if="item.age<25">
    <h5>{{item.name}}</h2>
    <p>年齡:{{item.age}}</p>
  </li>
</ul>
</div>

<script>
var app = new Vue({
  el: '#app',
  data: {
    list: [
      {
        name: '小明',
        age: 16
      },
      {
        name: '媽媽',
        age: 38,
      },
      {
        name: '漂亮阿姨',
        age: 24
      }
    ]
  }
})
</script>
```
### v-on
可縮寫成`＠`
```
<button class="btn btn-primary mt-1" @click="reverseText">轉字串</button>
```
> v-on == addEventListener
```
<div id="app">
  <input type="text" class="form-control" v-model="text"> // 雙向綁定
  <button class="btn btn-primary mt-1" v-on:click="reverseText">轉字串</button> // v-on：事件＝"執行函式"
  <div class="mt-3">
    {{ newText }}
  </div>
</div>

<script>
var app = new Vue({
  el: '#app',
  data: {
    text: '',
    newText: ''
  },
  methods: {
      reverseText(params) {  // 不用寫 function
      console.log(this.text);
      this.newText=this.text.split('').reverse().join('')
    }
  },
});
</script>
```
### v-class
> v-class == addClass
```
<div id="app">
  <div class="box" :class="{'rotate':isTransform}"></div> 
  //{'加入class名稱': true or false ，可加入判斷式}
  <hr>
  <button class="btn btn-outline-primary" @click="isTransform = !isTransform">轉物件</button>
</div>

<script>
var app = new Vue({
  el: '#app',
  data: {
    isTransform: false
  },
});
</script>
<style>
.box {
  transition: transform .5s;
}
.box.rotate {
  transform: rotate(45deg)
}
</style>
```
## Vue component
 Vue.component('自定義名稱',{})
```
<div id="app">
  <div>
    你已經點擊 <button class="btn btn-outline-secondary btn-sm" @click="counter += 1">{{ counter }}</button> 下。
  </div>
  <counter-component></counter-component> 
</div>

<script>
// 請在此撰寫 JavaScript
Vue.component('counter-component', {
// 取用的功能
  data:function(){ 
    return {counter: 0}
  },
// 顯現的方式
  template:`
  <button class="btn btn-outline-secondary btn-sm" @click="counter += 1">{{ counter }}</button>
  `
})

let app = new Vue({
  el: '#app',
  data: {
    counter: 0
  },
});
</script>
```
