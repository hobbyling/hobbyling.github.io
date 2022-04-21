---
title: 陣列批次操作
date: 2022-03-15 23:47:07
author: Hobby Lee
img: ./assets/Javascript-ArrayBatchAction/cover.jpg
top: false
hide: false
cover: false
coverImg: ./assets/Javascript-ArrayBatchAction/cover.jpg
summary: 陣列的各種批次操作
categories: JavaScript
tags:
  - JavaScript
  - Array
---

## Array.forEach()

> 對每個元素執行動作

將陣列元素一個一個抓出來，帶入函數執行。陣列元素如果是物件可變更，不會產生新陣列

```javascript
let books = [
  { discount: 0.9, price: 200 },
  { discount: 0.8, price: 100 },
  { discount: 0.7, price: 600 },
];

books.forEach((book) => {
  book.total = book.discount * book.price;
});

console.log(books);
/* ======= result ======= 
[
  { discount: 0.9, price: 200, total: 180 },
  { discount: 0.8, price: 100, total: 80},
  { discount: 0.7, price: 600, total: 420},
]
=======================*/
```

---

## Array.map()

> 執行結果存到新陣列

將陣列元素一個一個抓出來，將執行結果存成另一個陣列

```javascript
numbers = [1, 2, 3, 4, 5];

new_array = numbers.map((num) => {
  return num * num;
});

console.log(new_array);
/* ======= result ======= 
[1,4,9,16,25]
=======================*/
```

---

## Array.filter()

> 留下符合條件的元素

根據函數回傳值（true/false），決定要不要把元素複製到新陣列

```javascript
numbers = [1, 2, 3, 4, 5];

new_array = numbers.filter((num) => {
  console.log(num);
  return num > 3;
});

console.log(new_array);
/* ======= result ======= 
1
2
3
4
5
[4,5]
=======================*/
```

---

## Array.find()

> 找到第一個符合條件的元素

根據函數回傳值（true/false），傳回第一個符合條件的元素（非陣列），不會遍尋所有值

```javascript
dnas = ["ATC", "AGC", "TTG", "AAA"];

find_tg = dnas.find((dna) => {
  console.log(dna);
  return dna.indexOf("TG") > -1;
});

console.log(find_tg, typeof find_tg);
/* ======= result ======= 
ATC
AGC
TTG
TTG, string
=======================*/
```

---

## Array.some()

> 判斷有元素符合條件

其中有元素符合條件回傳 true，遇到符合條件的元素就會停止，不會遍尋所有值

```javascript
numbers = [1, 2, 6, 3, 4, 5];

find_tg = numbers.some((dna) => {
  console.log(dna);
  return dna > 3;
});

console.log(find_tg);
/* ======= result ======= 
1
2
6
true
=======================*/
```

---

## Array.every()

> 判斷所有元素都符合條件

每一個元素都符合條件回傳 true，遇到不符合條件的元素就會停止，不會遍尋所有值

```javascript
numbers = [1, 2, 6, 3, 4, 5];

find_tg = numbers.every((dna) => {
  console.log(dna);
  return dna > 3;
});

console.log(find_tg);
/* ======= result ======= 
1
false
=======================*/
```

---

## Array.sort()

> 根據大小排列陣列

根據函數回傳值排列陣列

```javascript
nums = [6, 4, 9, 3];
nums.sort();

console.log(nums);
/* ======= result ======= 
[3, 4, 6, 9]
=======================*/
```

---

## Array.reduce(函數, 初始值)

> 根據規則縮減陣列

根據取出每個值與暫存做運算，回傳結果
Eg. 把書籍價錢加到暫存裡 -> 總價

```javascript
books = [{ price: 10 }, { price: 20 }, { price: 30 }];

let total = books.reduce(function (total, a) {
  return total + a.price;
}, 0);

console.log(total);
/* ======= result ======= 
60
=======================*/
```

---

Cover: Photo by Kelli Tungay on [Unsplash](https://unsplash.com/photos/2LJ4rqK2qfU)
