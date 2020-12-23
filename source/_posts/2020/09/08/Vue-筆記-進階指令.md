---
title: 'Vue 筆記 進階指令 '
tags:
  - Vue
category: Vue
abbrlink: 23984
date: 2020-09-08 15:08:17
---
## 進階指令
### v-class
button v-on
input v-model

```
<div id="app">
  <h4>物件寫法</h4>
  <div class="box" :class="{'rotate':isTransform,'bg-danger':boxColor}"></div>
  <p>請為此元素加上動態 className</p>
  <hr>
  <button class="btn btn-outline-primary" @click="isTransform = !isTransform">選轉物件</button>
  <div class="form-check">
    <input type="checkbox" class="form-check-input" id="classToggle1" v-model="boxColor">
    <label class="form-check-label" for="classToggle1">切換色彩</label>
  </div>
  <hr>
  <h5>物件寫法 2</h5>
  <div class="box" :class="objectClass"></div>
  <p>請將此範例改為 "物件" 寫法</p>
  <hr>
  <button class="btn btn-outline-primary" @click="objectClass.rotate =!objectClass.rotate">選轉物件</button>
  <div class="form-check">
    <input type="checkbox" class="form-check-input" id="classToggle2" v-model="objectClass['bg-danger']">
    <label class="form-check-label" for="classToggle2">切換色彩</label>
  </div>
  <hr>
  <h4>陣列寫法</h4>
  <button class="btn" :class="arrayClass">請操作本元件</button>
  <p>請用陣列呈現此元件 className</p>
  <div class="form-check">
    <input type="checkbox" class="form-check-input" id="classToggle3" v-model="arrayClass" value="btn-outline-primary">  
    <label class="form-check-label" for="classToggle3">切換樣式</label>
  </div>
  <div class="form-check">
    <input type="checkbox" class="form-check-input" id="classToggle4" v-model="arrayClass" value="active">
    <label class="form-check-label" for="classToggle4">啟用元素狀態</label>
  </div>
  <hr>
  <h4>綁定行內樣式</h4>
  <p>請用不同方式綁定以下行內樣式</p>
  <div class="box" :style="styleObject"></div>
  <div class="box" :style="[styleObject,styleObject2,styleObject3]"></div>
  <div class="box" :style="{backgroundColor: styleObject2.boxShadow}"></div>
  <hr>
  <h5>自動加上 Prefix (每個版本結果不同)</h5>
  <div class="box" :class="styleObject3"></div>
</div>

<script>
var app = new Vue({
  el: '#app',
  data: {
    isTransform: false,
    boxColor: false,
    objectClass: {
      'rotate': false,
      'bg-danger': false,
    },

    // Array 操作
    arrayClass: [],

    // 行內樣式
    // 使用駝峰式命名
    styleObject: {
      backgroundColor: 'red',
      borderWidth: '5px'
    },
    styleObject2: {
      boxShadow: '3px 3px 5px rgba(0, 0, 0, 0.16)'
    },
    styleObject3: {
      userSelect: 'none'
    }
  },
});
</script>

<style>
.box {
  transition: all .5s;
}
.box.rotate {
  transform: rotate(45deg)
}
</style>
```
### v-for
v-for 加上 key 綁id
修改陣列資料`Vue.set(array,index,value)`
```
<div id="app">
  <h4>陣列與物件的迴圈</h4>
  <p>請使用 v-for 在陣列與物件上，並且加上索引</p>
  <ul>
    <li v-for="(item, key) in objectData">
      {{ key }} - {{ item.name }} {{ item.age }} 歲
    </li>
  </ul>
  <ul>
    
  </ul>
  <hr>
  <h4>Key</h4>
  <p>請在範例上補上 key，並觀察其差異</p>
  <ul>
    <li v-for="(item, key) in arrayData":key="item.age">
      {{ key }} - {{ item.name }} {{ item.age }} 歲 <input type="text">
    </li>
  </ul>
  <button class="btn btn-outline-primary" @click="reverseArray">反轉陣列</button>

  <h4>Filter</h4>
  <p>請製作過濾資料</p>
  <input type="text" class="form-control" v-model="filterText" @keyup.enter="filterData">
  <ul>
    <li v-for="(item, key) in arrayData" :key="item.age">
      {{ key }} - {{ item.name }} {{ item.age }} 歲 <input type="text">
    </li>
  </ul>

  <h4>不能運作的狀況</h4>
  <p>講師說明</p>
  <button class="btn btn-outline-primary" @click="cantWork">無法運行</button>
  <ul>
    <li v-for="(item, key) in arrayData" :key="item.age">
      {{ key }} - {{ item.name }} {{ item.age }} 歲 <input type="text">
    </li>
  </ul>

  <h4>純數字的迴圈</h4>
  <ul>
    <li v-for="item in 10">
      {{ item }}
    </li>
  </ul>

  <h4>Template 的運用</h4>
  <p>請將兩個 tr 一組使用 v-for</p>
  <table class="table" v-for="(item, index) in arrayData" :key="index">
    <template>
      <tr>
        <td>{{item.age}}</td>
      </tr>
      <tr>
        <td>{{item.name}}</td>
      </tr>

    </template>
  </table>

  <h4>v-for 與 v-if</h4>
  <p>請加上 v-if 判斷式</p>
  <ul>
    <li v-for="(item, key) in arrayData" v-if="item.age>20">
      {{ key }} - {{ item.name }} {{ item.age }} 歲
    </li>
  </ul>

  <h4>v-for 與 元件</h4>
  <p>講師說明</p>
  <ul>
    <list-item :item="item" v-for="(item, key) in arrayData" :key="key"></list-item>
  </ul>
  <p>注意：現在建議元件使用 v-for 都加上 key。<a href="https://cn.vuejs.org/v2/guide/list.html#%E4%B8%80%E4%B8%AA%E7%BB%84%E4%BB%B6%E7%9A%84-v-for">參考</a></p>
</div>

<script>
Vue.component('list-item', {
  template: `
    <li>
      {{ item.name }} {{ item.age }} 歲
    </li>
  `,
  props: ['item']
});

var app = new Vue({
  el: '#app',
  data: {
    arrayData: [
      {
        name: '小明',
        age: 16
      },
      {
        name: '漂亮阿姨',
        age: 24
      },
      {
        name: '杰倫',
        age: 20
      }
    ],
    objectData: {
      ming: {
        name: '小明',
        age: 16
      },
      auntie: {
        name: '漂亮阿姨',
        age: 24
      },
      jay: {
        name: '杰倫',
        age: 20
      }
    },
    filterArray: [],
    filterText: ''
  },
  methods: {
    // 請在此練習 JavaScript

    // 解答：
    reverseArray: function () {
      this.arrayData.reverse()
      console.log(this.arrayData)
    },
    filterData: function () {
      var vm = this;
      vm.filterArray = vm.arrayData.filter(function (item) {
        console.log(vm.filterText, item.name, item.name.match(vm.filterText))
        return item.name.match(vm.filterText);
      });
    },
    cantWork: function () {
      // // 情境一
      // this.arrayData.length = 2;

      // 情境二
      this.arrayData[0] = {
        name: '阿強',
        age: 99
      }
      //解法
      Vue.set(this.arrayData, 0, {
        name: '阿強',
        age: 99
      })
      console.log(this.arrayData)
    }
  }
});
</script>
```
### v-if v-else-if v-else
v-if 移除整個 `DOM`
v-show `display:none`
```
<div id="app">
  <h4>v-if, v-else</h4>
  <p>使用 v-if, v-else 切換物件呈現</p>
  <div class="alert alert-success" v-if="isSuccess">成功!</div>
  <div class="alert alert-danger" v-else>失敗!</div>
  <div class="form-check">
    <input type="checkbox" class="form-check-input" id="isSuccess" v-model="isSuccess">
    <label class="form-check-label" for="isSuccess">啟用元素狀態</label>
  </div>

  <h4>template 標籤</h4>
  <p>使用 template 切換多數 DOM 呈現</p>
  <table class="table">
    <thead>
      <th>編號</th>
      <th>姓名</th>
    </thead>
  <template v-if="showTemplate">
      <tr>
        <td>1</td>
        <td>安妮</td>
      </tr>
      <tr>
        <td>2</td>
        <td>小明</td>
      </tr>
  </template>
</table>
  <div class="form-check">
    <input type="checkbox" class="form-check-input" id="showTemplate" v-model="showTemplate">
    <label class="form-check-label" for="showTemplate">啟用元素狀態</label>
  </div>
  <hr>
  <h4>v-else-if</h4>
  <p>使用 v-else-if 做出分頁頁籤</p>
  <ul class="nav nav-tabs">
    <li class="nav-item">
      <a class="nav-link" href="#" @click.prevent="link='a'" :class="{'active': link === 'a'}">標題一</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#" @click.prevent="link='b'" :class="{'active': link === 'b'}">標題二</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#" @click.prevent="link='c'" :class="{'active': link === 'c'}">標題三</a>
    </li>
  </ul>
  <div class="content">
    <div v-if="link === 'a'">Ａ</div>
    <div v-else-if="link === 'b'">Ｂ</div>
    <div v-else-if="link === 'c'">Ｃ</div>
  </div>
  <hr>
  <h4>KEY</h4>
  <p>講師說明 Vue 切換狀態可能遇到的問題</p>
  <template v-if="loginType === 'username'">
    <label>Username</label>
    <input class="form-control" placeholder="Enter your username" :key="1">
  </template>
  <template v-else>
    <label>Email</label>
    <input class="form-control" placeholder="Enter your email address" :key="2">
  </template>
  <button class="btn btn-outline-primary mt-3" @click="toggleLoginType" >切換狀態</button>
  <hr>
  <h4>v-if 與 v-show</h4>
  <p>講師說明 v-if 與 v-show 的差異</p>
  <div class="alert alert-success" v-show="isSuccess">成功!</div>
  <div class="alert alert-danger" v-show="!isSuccess">失敗!</div>
  <div class="form-check">
    <input type="checkbox" class="form-check-input" id="isSuccess2" v-model="isSuccess">
    <label class="form-check-label" for="isSuccess2">啟用元素狀態</label>
  </div>
</div>

<script>
var app = new Vue({
  el: '#app',
  data: {
    isSuccess: true,
    showTemplate: true,

    link: 'a',

    loginType: 'username'
  },
  methods: {
    toggleLoginType: function () {
      return this.loginType = this.loginType === 'username' ? 'email' : 'username'
    }
  }
});
</script>
```
### Computed Watch
Computed 是監聽整體資料變化
Watch 是監聽 `Vue` 變數變化
```
<div id="app">
  <h4>Computed</h4>
  <p>使用 Computed 來過濾資料。</p>
  <input type="text" class="form-control" v-model="filterText">
  <ul>
    <li v-for="(item, key) in filterArray" :key="item.age">
      {{ key }} - {{ item.name }} {{ item.age }} 歲 <input type="text">
    </li>
  </ul> 
  <p>使用 Computed 來呈現時間格式。</p>
  <p>{{formatTime}}</p>
  <h4>Watch</h4>
  <p>使用 trigger 來觸發旋轉 box、並在三秒後改變回來</p>
  <div class="box" :class="{'rotate': trigger }"></div>
  <hr>
  <button class="btn btn-outline-primary" @click="openTrigger">Counter</button>
</div>

<script>
var app = new Vue({
  el: '#app',
  data: {
    arrayData: [
      {
        name: '小明',
        age: 16
      },
      {
        name: '漂亮阿姨',
        age: 24
      },
      {
        name: '杰倫',
        age: 20
      }
    ],
    filterText: '',
    trigger: false,
    newDate: 0
  },
  methods: {
    openTrigger: function() {
      var vm = this;
      vm.trigger = true
    },
    closeTrigger: function() {
      var vm = this;
      setTimeout(function() { 
        vm.trigger = false
      }, 3000);
    }
  },
  watch: {
    trigger: function() {
      this.closeTrigger();
    }
  },
  computed: {
    filterArray: function () {
      var vm = this;
      return vm.arrayData.filter(function(item) {
        return item.name.match(vm.filterText);
      });
    },
    formatTime: function () {
      console.log(this.newDate)
      var dates = new Date(this.newDate * 1000);
      var year = dates.getFullYear();
      var month = dates.getMonth() + 1;
      var date = dates.getDate() + 1;
      var hours = dates.getHours();
      var minutes = dates.getMinutes();
      var seconds = dates.getSeconds();
      return `${year}/${month}/${date} ${hours}:${minutes}:${seconds}`
    }
  },
  mounted: function () {
    this.newDate = Math.floor(Date.now() / 1000);
  }

});
</script>

<style>
.box {
  transition: all .5s;
}
.box.rotate {
  transform: rotate(45deg)
}
</style>
```
### 表單細節操作
`select`+`multiple` = 複選
##### 修飾符
v-model.lazy =離開元素才會顯現
v-model.number =value轉數字
v-model.trim =最後不留白
```
<div id="app">
  <h4>Select</h4>
  <select name="" id="" class="form-control" v-model="selected">
    <option disabled value="">請選擇</option>
    <option value="小美">小美</option>
    <option value="可愛小妞">可愛小妞</option>
    <option value="漂亮阿姨">漂亮阿姨</option>
  </select>
  <p>小明喜歡的女生是 {{ selected }}。</p>
  <hr>
  <select name="" id="" class="form-control" v-model="selected2" >
    <option disabled value="">請選擇</option>
    <option :value="item" v-for="(item, index) in selectData" :key="index">{{item}}</option>
  </select>
  <p>小明喜歡的女生是 {{ selected2 }}。</p>
  <hr>
  <h4 class="mt-3">多選</h4>
  <select name="" id="" class="form-control" multiple v-model="multiSelected" >
    <option value="小美">小美</option>
    <option value="可愛小妞">可愛小妞</option>
    <option value="漂亮阿姨">漂亮阿姨</option>
  </select>
  <p>小明喜歡的女生是 <span v-for="item in multiSelected">{{ item }} </span>。</p>
  <hr>
  <h4 class="mt-3">複選框</h4>
  <div class="form-check">
    <input type="checkbox" class="form-check-input" id="sex" v-model="sex" true-value="boy" false-value="girl">
    <label class="form-check-label" for="sex">{{ sex }}</label>
  </div>
  <h4 class="mt-3">修飾符</h4>
  {{ lazyMsg }}
  <input type="text" class="form-control" v-model.lazy="lazyMsg">
  <br>
  <pre>{{ age }}</pre>
  <input type="number" class="form-control" v-model.number="age">
  <br>
  {{ trimMsg }}緊黏的文字
  <input type="text" class="form-control" v-model.trim="trimMsg">
</div>

<script>
var app = new Vue({
  el: '#app',
  data: {
    singleRadio: '',
    selected: '',
    selectData: ['小美', '可愛小妞', '漂亮阿姨'],
    selected2: '',
    multiSelected: [],
    sex: '男生',

    // 修飾符
    lazyMsg: '',
    age: '',
    trimMsg: ''
  },
});
</script>
```
### v-on
```
<div id="app">
  <p>請切換下方 box 的 className</p>
  <div class="box" :class="{'rotate': isRotate }"></div>
  <hr>
  <button class="btn btn-outline-primary" @click="changeRotate">切換 box 樣式</button>
  <hr>
  <h4>帶入參數</h4>
  <ul>
    <li v-for="item in arrayData" class="my-2">
      {{ item.name }} 有 {{ item.cash }} 元 
      <button class="btn btn-sm btn-outline-primary" @click="storeMoney(item)">儲值</button>
    </li>
  </ul>
  <h4>修飾符</h4>
  <h5>事件修飾符</h5>
  <ul>
    <li>.stop - 調用 event.stopPropagation()。</li>
    <li>.prevent - 調用 event.preventDefault()。</li>
    <li>.capture - 添加事件偵聽器時使用 capture 模式。</li>
    <li>.self - 只當事件是從偵聽器綁定的元素本身觸發時才觸發回調。</li>
    <li>.once - 只觸發一次回調。</li>
  </ul>

  <h5>按鍵修飾符</h5>
  <ul>
    <li>.{keyCode | keyAlias} - 只當事件是從特定鍵觸發時才觸發回調。</li>
    <li>別名修飾 - .enter, .tab, .delete, .esc, .space, .up, .down, .left, .right</li>
    <li>修飾符來實現僅在按下相應按鍵時才觸發鼠標或鍵盤事件的監聽器 - .ctrl, .alt, .shift, .meta</li>
  </ul>
  <h6 class="mt-3">keyCode</h6>
  <input type="text" class="form-control" v-model="text" @keyup.enter="trigger(13)">

  <h6 class="mt-3">別名修飾</h6>
  <input type="text" class="form-control" v-model="text" @keyup.space="trigger('space')">

  <h6 class="mt-3">相應按鍵時才觸發的監聽器</h6>
  <input type="text" class="form-control" v-model="text" @keyup.shift.enter="trigger('shift + Enter')">
  
  <h5>滑鼠修飾符</h5>
  <ul>
    <li>.left - (2.2.0) 只當點擊鼠標左鍵時觸發。</li>
    <li>.right - (2.2.0) 只當點擊鼠標右鍵時觸發。</li>
    <li>.middle - (2.2.0) 只當點擊鼠標中鍵時觸發。</li>
  </ul>
  <h6 class="mt-3">滑鼠修飾符</h6>
  <div class="p-3 bg-primary">
    <span class="box" @click.left="trigger('Right button')">
    </span>
  </div>
</div>

<script>
var app = new Vue({
  el: '#app',
  data: {
    arrayData: [
      {
        name: '小明',
        age: 16,
        cash: 500
      },
      {
        name: '漂亮阿姨',
        age: 24,
        cash: 1000
      },
      {
        name: '杰倫',
        age: 20,
        cash: 5000
      }
    ],
    isRotate: false,
    text: ''
  },
  methods: {
    changeRotate: function() {
      this.isRotate = !this.isRotate;
    },
    storeMoney: function(item) {
      item.cash = item.cash + 500;
    },
    trigger: function(name) {
      console.log(name, '此事件被觸發了')
    }
  }
  // 解答
});
</script>

<style>
.box {
  display: block;
  transition: all .5s;
}
.box.rotate {
  transform: rotate(45deg)
}
</style>
```
