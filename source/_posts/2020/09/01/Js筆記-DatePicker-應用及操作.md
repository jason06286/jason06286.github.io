---
title: 'Js筆記 DatePicker 應用及操作 '
tags:
  - JavaScript
  - Datepicker
category: JavaScript
abbrlink: 8450
date: 2020-09-01 16:13:16
---
# DatePicker
日曆選擇器在 [BootStrap](https://bootstrap-datepicker.readthedocs.io/en/latest/)或 [jQuery UI](https://jqueryui.com/datepicker/) 等其實都已經有相關的套件，不過這次是使用[Date Range Picker](https://www.daterangepicker.com/#options)
，因為要使用在訂房網上，所以需要用到選取範圍功能。
## [Date Range Picker](https://www.daterangepicker.com/#options)
### 開始使用
只要至[官網](https://www.daterangepicker.com/#usage)插入 `cdn` 或下載檔案下來，
並宣告`.daterangepicker();`即可使用。
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="https://cdn.jsdelivr.net/jquery/latest/jquery.min.js"></script>
    <script type="text/javascript" src="https://cdn.jsdelivr.net/momentjs/latest/moment.min.js"></script>
    <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/daterangepicker/daterangepicker.min.js"></script>
    <link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/npm/daterangepicker/daterangepicker.css" />
</head>
<body>
    <input type="text" class="date">
    <script>
        $('.date').daterangepicker()
    </script>
</body>
</html>
```
### 常用選項
```
$('.date').daterangepicker({
    "startDate":開始日期,
    "endDate": 結束日期,
    "locale": {
        "format": "YYYY年MM月DD日", // 日期格式
        "separator": " - ",
        "applyLabel": "確認",  //自定義 apply 按鈕名稱
        "cancelLabel": "取消", //自定義 cancel 按鈕名稱
        "daysOfWeek": [   //自定義星期名稱
            "日",
            "一",
            "二",
            "三",
            "四",
            "五",
            "六"
        ],
        "monthNames": [       //自定義月份名稱
            "1 月",
            "2 月",
            "3 月",
            "4 月",
            "5 月",
            "6 月",
            "7 月",
            "8 月",
            "9 月",
            "10 月",
            "11 月",
            "12 月"
        ],
        "firstDay": 1  //自定義開始星期，0為星期日 
    },
})
```
### 客製化
因為有太多功能可以選擇，官網下方也有 UI 介面，供大家客製化選擇。
> [開始客製化日期選擇器](http://www.daterangepicker.com/#config)

![](/images/datepicker/datepicker.png)
## 如何取出日期範圍的值
我們可以利用 `while` 迴圈，再利用 `new Date()`產生日期格式。
```
const getDatesBetween = (startDate, endDate) => {
        let reserveDayData=[] 
        let result=[] 
        let currentDate = startDate
        let holiday=0
        let weekday=0
        console.log(startDate,endDate)
        while(currentDate < endDate){ //開始日期＋1天 < 結束日期
            reserveDayData.push(new Date(currentDate))
            // 台北時間跟國際時間差八小時
            result.push(new Date(currentDate+ 8 * 3600 * 1000).toISOString().split("T")[0]) 
            // 現在日期加一天
            currentDate = moment(currentDate).add(1, 'days'); 
        }
        console.log(reserveDayData)
		console.log(result)
        // 計算幾晚
        // 最後一天沒住，所以扣除
		reserveDayData.pop()
        reserveDayData.forEach(function (item) {
            if(item.getDay()===0 ||item.getDay()===6){
                    return holiday+=1
            }else{
                    return weekday+=1
            }
		})
        console.log(holiday)  
		console.log(weekday)
	}
```
## 範例
* [DEMO](https://jason06286.github.io/bookingPractice/index.html)
* [GitHub](https://github.com/jason06286/bookingPractice)

