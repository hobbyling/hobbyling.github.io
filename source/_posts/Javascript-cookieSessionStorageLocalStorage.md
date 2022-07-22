---
title: Cookie, SessionStorage 與 LocalStorage 差異
date: 2022-07-11 23:56:31
author: Hobby Lee
img: ./assets/Javascript-cookieSessionStorageLocalStorage/cover.jpg
top: true
hide: false
cover: true
coverImg: ./assets/Javascript-cookieSessionStorageLocalStorage/cover.jpg
summary: JavaScript Cookie, SessionStorage 與 LocalStorage 三者差異
categories: JavaScript
tags:
  - JavaScript
---

client 端將資料存在瀏覽器的方式有三種，分別為 cookie, SessionStorage 與 LocalStorage。
而這三種方式皆有些許差異，因此筆記下來

## <font color=#ee6e73> :herb: Cookie</font>

### 特性

- 獨立於域名
  - 舉例: 在*.aaa.com存入的 cookie，不會出現在*.bbb.com
- 可設定失效時間
  - 預設是關閉瀏覽器後失效
- 有個數限制（各瀏覽器不同），一般不能超過20個
- 儲存型別：String
- 儲存位置
  - 未設定過期時間：存在記憶體中，瀏覽器關閉後銷燬
  - 設定過期時間：存在系統硬碟中，直到過期時間結束後才消失（即使關閉瀏覽器）
- 會被附加在每一次的 request 中，可能會影響效能
  - ![Cookie 會附加在每一次的 request 中](./assets/Javascript-cookieSessionStorageLocalStorage/01.jpg)

### 缺點

- 所有資料在 Client 端就可以被修改
- 儲存量小（約 4KB），資料字段太多會影響傳輸效率

### 應用場景

- token，認證身份，例如登入狀態、購物車
- 追蹤使用者及廣告
- 記住密碼功能、自動登入
- 儲存登入時間、瀏覽次數等資訊

---

## <font color=#ee6e73> :herb: SessionStorage</font>

### 特性

- 儲存量較大（約 5MB）
- 預設不會逾期，每次分頁或瀏覽器關掉後就會清除
- 獨立於域名
- 生命周期只存在瀏覽囂的單一分頁
  - 另開新分頁的話，又是一個新的sessionStorage
  - 舉例: 在 aaa.com/page1 存入的 SessionStorage，不會出現在 aaa.com/page2
  - 子域名相互不能訪問對方的儲存物件
- 儲存型別：String
- 每次 request 不會帶上

### 應用場景

- 敏感賬號一次性登入，如網銀

---

## <font color=#ee6e73> :herb: LocalStorage</font>

### 特性
- 儲存量較大（約 5mb）
- 不會逾期，除非手動清除
- 獨立於域名
- 生命週期存在所有特定域名下
  - 跨瀏覽器分頁、新視窗、甚至是關閉瀏覽器後再打開，localStorage仍然會存在
  - 舉例: 在 aaa.com/page1 存入的 LocalStorage，會出現在 aaa.com/page2
  - 子域名相互不能訪問對方的儲存物件
- 儲存型別：String
- 每次 request 不會帶上

### 應用場景

- 瀏覽器對該頁面的訪問次數
- 購物車資訊
- 記住密碼功能、長期登入

### 提取方式

```javascript
// 設定資料
windows.localStorage.setItem(key, value)

// 取得資料
let stroage = windows.localStorage.getItem(key)

// 刪除資料
windows.localStorage.removeItem(key, value)

// 刪除全部資料
windows.localStorage.clear()
```

### 設定過期時間

```javascript
function store(key,value,expire) {
    let obj = {
        time:new Date().getTime(),
        value:value,
        expire:expire,
    }
    //localStorage只能儲存字串，所以要先將物件轉成字串
    let objStr = JSON.stringify(obj);
    localStorage.setItem(key,objStr);
}
//儲存name,名稱為'hxj',過期時間為5000毫秒
store('name','hxj',5000);
var timer = setInterval(function () {
    if(localStorage.getItem('name')){
        var name = localStorage.getItem('name');
        var nameObj = JSON.parse(name);
        console.log(new Date().getTime() - nameObj.time);
        if(new Date().getTime() - nameObj.time >= nameObj.expire){
            localStorage.removeItem('name')
        }
    }else{
        alert('localStorage已失效');
        clearInterval(timer);
    }
},1000)
```

---

## <font color=#ee6e73> :herb: 比較表</font>

|  特性     | Cookie  |  SessionStorage  | LocalStorage  |
|  :----:  | ----  | ----  | ----  |
| 生命週期   | 可設定失效時間。預設是關閉瀏覽器後失效 | 關閉頁面或瀏覽器後被清除 | 除非被清除，否則永久保存 |
| 大小      | 4KB 左右 | 一般為 5MB | 一般為 5MB |
| 與 Server 溝通  | 每次都會攜帶在 HTTP 中，保存過多資料會帶來效能問題 | 僅在瀏覽器保存，不參與 Server 的溝通 | 僅在瀏覽器保存，不參與 Server 的溝通 |

---

## <font color=#ee6e73> :herb: 參考資料</font>

- [Javascript怎樣使用SessionStorage和LocalStorage](https://www.796t.com/article.php?id=278352)
- [JavaScript Cookie、LocalStorage、SessionStorage 差異 | by Peggy Chan | Medium](https://medium.com/@bebebobohaha/cookie-localstorage-sessionstorage-%E5%B7%AE%E7%95%B0-9e1d5df3dd7f)
- [第八週網頁資料儲存 — cookie、local Storage、Session Storage | by Miahsu | Medium](https://miahsuwork.medium.com/%E7%AC%AC%E5%85%AB%E9%80%B1-%E7%B6%B2%E9%A0%81%E8%B3%87%E6%96%99%E5%84%B2%E5%AD%98-cookie-local-storage-session-storage-a3f40013da37)

---

cover: Photo by <a href="https://unsplash.com/photos/UvRMcIeXq9Y">Aaron Burden</a> on <a href="https://unsplash.com/">Unsplash</a>