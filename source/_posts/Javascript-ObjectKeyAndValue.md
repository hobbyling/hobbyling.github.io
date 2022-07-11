---
title: 取得物件的 key / value 值
date: 2022-03-24 22:57:53
author: Hobby Lee
img: ./assets/Javascript-ObjectKeyAndValue/cover.jpg
top: false
hide: false
cover: true
coverImg: ./assets/Javascript-ObjectKeyAndValue/cover.jpg
summary: 取得物件的 key 或者 value 值
categories: JavaScript
tags:
  - JavaScript
  - Object
---

## <font color=#ee6e73> :herb: Object.keys()</font>

> 將物件中的 key 值，排序並以陣列回傳

- 範例一

```javascript
let obj = { a: 1, b: 2, c: 3 };

console.log(Object.keys(obj));

/* ======= result ======= 
 ['a', 'b', 'c']
=======================*/
```

- 範例二：排序

```javascript
let obj = { 1: "a", 0: "b", 2: "c", 4: "d", 3: "e" };

console.log(Object.keys(obj));

/* ======= result ======= 
 ['0', '1', '2', '3', '4']
=======================*/
```

---

## <font color=#ee6e73> :herb: Object.values()</font>

> 將物件中的 value 值，根據 key 值做排序並以陣列回傳

- 範例一

```javascript
let obj = { a: 1, b: 2, c: 3 };

console.log(Object.values(obj));

/* ======= result ======= 
 [1, 2, 3]
=======================*/
```

- 範例二：排序

```javascript
let obj = { 1: "a", 0: "b", 2: "c", 4: "d", 3: "e" };

console.log(Object.values(obj));

/* ======= result ======= 
 ['b', 'a', 'c', 'e', 'd']
=======================*/
```

- 範例三：填入字串，會將字串分割成陣列

```javascript
const string = "hobby";
console.log(Object.values(string));
/* ======= result ======= 
 ['h', 'o', 'b', 'b', 'y']
=======================*/
```

- 範例三：填入 Boolean，會回傳空陣列

```javascript
const boo = true;
console.log(Object.values(boo));
/* ======= result ======= 
 []
=======================*/
```

---

## <font color=#ee6e73> :herb: Object.entries()</font>

> 取得物件中的 key 和 value，根據 key 值做排序並以陣列回傳

- 範例一

```javascript
let obj = { a: 1, b: 2, c: 3 };

console.log(Object.entries(obj));

/* ======= result ======= 
[ 
  ['a', 1],
  ['b', 2],
  ['c', 3]
]
=======================*/
```

- 範例二：排序

```javascript
let obj = { 1: "a", 0: "b", 2: "c", 4: "d", 3: "e" };

console.log(Object.entries(obj));

/* ======= result ======= 
[ 
  ['0', 'b'],
  ['1', 'a'],
  ['2', 'c'],
  ['3', 'e'],
  ['4', 'd'] 
]
=======================*/
```

## <font color=#ee6e73> :herb: 皆不會迭代到繼承的 property</font>

> 從別人那邊繼承過來的 property，在使用以上三種方法時，結果並不會被列出

- width 和 height 並沒有被印出來

```javascript
let size = { width: 20, height: 50 };

let customSize = Object.create(size);
customSize.color = "red";
customSize.name = "Custom";

Object.keys(customSize).forEach((key) => {
  console.log(key, customSize[key]);
});

/* ======= result ======= 
color red
name Custom
=======================*/

Object.entries(customSize).forEach(([key, value]) => {
  console.log(key, value);
});

/* ======= result ======= 
color red
name Custom
=======================*/
```

---

## <font color=#ee6e73> :herb: 參考資料</font>

- [JavaScript 之旅 (4)：Object.keys() & Object.values() & Object.entries()](https://titangene.github.io/article/javascript-object-keys-values-entries.html)
- [JavaScript Object.values()用法及代碼示例](https://vimsky.com/zh-tw/examples/usage/javascript_library_object_values.html)

---

cover: Photo by Cristina Graf Adamoli on [Unsplashn](https://unsplash.com/photos/ELM74Lhmyfo)
