---
title: 浮點數陷阱
date: 2022-07-22 09:52:35
author: Hobby Lee
img: ./assets/Javascript-FloatTrap/cover.jpg
top: false
hide: false
cover: false
coverImg: ./assets/Javascript-FloatTrap/cover.jpg
summary: 浮點數運算時遇到的小坑
categories: JavaScript
tags:
  - JavaScript
  - Float
---

在進行運算時，很理所當然的認為 10 - 9.99 = 0.01，但實作時卻一直發生錯誤。
console 出來後發現，與原本預想的結果不相同，因此花了一些時間了解其中的原因。

```JavaScript
// 預期結果
10 - 9.99 = 0.01
```

```JavaScript
// 實際結果
10 - 9.99 = 0.009999999999999787
```

---

## <font color=#ee6e73> :herb: 原因</font>

JavaScript 中的所有數字，包含整數及小數，都是 `Number` 型別，並遵循 IEEE 754 標準，使用 64 位固定長度表示。此做法的優點是歸一化處理整數和小數，節省存盤空間。

我們平常學習的運算方式，是使用十進制處理。
然而 JavaScript 是先使用二進制來計算後，再轉換成十進制。浮點數再轉乘二進制造成無窮迴圈，進而產生誤差。

### JavaScript 計算步驟

- 先將數字轉成二進制

```
10 => 1010

9.99 => 1001.1111110101110000101000111101011100001010001111011
```

- 運算

```
1010 - 1001.1111110101110000101000111101011100001010001111011 
= 0.0000001010001111010111000010100011110101110000101
```

- 轉成十進制

```
0.0000001010001111010111000010100011110101110000101 => 0.009999999999999787
```

---

## <font color=#ee6e73> :herb: 解法</font>


### 1. 先乘以 100，四捨五入後再除以 100

需求為取至小數點後兩位時

```JavaScript
let num = ((Number(10) * 100) - (Number(9.99) * 100)) / 100

Math.floor(num * Math.pow(10, 2)) / Math.pow(10, 2)
```

### 2. toPrecision(12)

12 能解決掉大部分 0001 和 0009 的問題

```JavaScript
parseFloat(1.4000000000000001.toPrecision(12)) === 1.4  // True
```


---

## <font color=#ee6e73> :herb: 參考資料</font>

- [js 浮點數陷阱](https://www.uj5u.com/qiye/246476.html)
- [JavaScript-Number的各種地雷--浮點數運算](https://ad57475747.medium.com/javascript%E6%B5%AE%E9%BB%9E%E6%95%B8%E9%81%8B%E7%AE%97-1691eefe3ea7)
- [javascript浮點數的陷阱](https://tso1158687.github.io/blog/2018/12/17/javascript-float-trap/)

---

Photo by <a href="https://unsplash.com/es/@evieshaffer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Evie S.</a> on <a href="https://unsplash.com/@evieshaffer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  
  