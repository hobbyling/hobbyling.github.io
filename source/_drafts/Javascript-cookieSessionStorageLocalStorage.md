---
title: Cookie, Session Storage 與 Local Storage 差異
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

- 由瀏覽器處理
- 只在特定網域內有用
  - 舉例: 在*.aaa.com存入的 cookie，不會出現在*.bbb.com
- 可設定失效時間
  - 預設是關閉瀏覽器後失效
- 有個數限制（各瀏覽器不同），一般不能超過20個
- 會被附加在每一次的 request 中，可能會影響效能
  - ![Cookie 會附加在每一次的 request 中](./assets/Javascript-cookieSessionStorageLocalStorage/01.jpg)

### 缺點

- 所有資料在 Client 端就可以被修改
- 儲存量小（約 4kb），資料字段太多會影響傳輸效率

### 應用場景

- 認證身份，例如登入狀態、購物車
- 追蹤使用者及廣告
- 記住密碼功能

---
## <font color=#ee6e73> :herb: Session Storage</font>