---
title: Js筆記 AJAX
tags: 
- JavaScript
- XMLHttpRequest
category: JavaScript
abbrlink: 41868
date: 2020-08-17 14:38:12
---
# AJAX
## XMLHttpRequest
### open 格式
![](/images/ajax/ajax1.png)
### onlaod
確定資料回傳，執行以下函式
```
function getData() {
    let xhr=new XMLHttpRequest();
    xhr.open('get',url,true);
    xhr.send(null);
    console.log(xhr.responseText)
    xhr.onload=function () { 
        let data1 = JSON.parse(xhr.responseText)
        return data=data1.ROOT.RECORD
}}
```
## asios
![](/images/ajax/ajax2.png)
```
// axios
function getData(){
    axios.get(url)
    .then(function (response) {
        return data=response.data.ROOT.RECORD
    });
}
```
## jQuery
![](/images/ajax/ajax3.png)
```
function getData() {
    $(document).ready(function () {
        $.ajax({
            type: "get",
            url: url,
            data: "data",
            dataType: "json",
            success: function (response) {
                return data=response.ROOT.RECORD
            }
        });
    });
}
```
[範例](https://codepen.io/jasonuse/pen/zYqBxzj?editors=0010)


