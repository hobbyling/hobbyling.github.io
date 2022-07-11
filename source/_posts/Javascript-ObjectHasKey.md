---
title: 判斷物件裡是否含有特定屬性
date: 2022-03-20 02:04:35
author: Hobby Lee
img: ./assets/Javascript-ObjectHasKey/cover.jpg
top: false
hide: false
cover: false
coverImg: ./assets/Javascript-ObjectHasKey/cover.jpg
summary: 判斷物件裡是否含有特定屬性
categories: JavaScript
tags:
  - JavaScript
  - Object
---

## <font color=#ee6e73> :herb: 情境</font>

在進行前端專案時，常會遇到後端回傳的 API 資料內，少了某個 key 值，導致程式報錯，畫面無法渲染。

可能因為該 key 值內沒有值，所以後端索性不給了。看起來資料是簡潔了許多，但是真的是非常困擾......

例如： Object 內少了一個 key favorite，導致 `v-if="favorite"` 時會報錯

```javascript
obj = {
  name: "Hobby",
  gender: "female",
  // favorite: 'bubble-tea'
};
```

## <font color=#ee6e73> :herb: 解法</font>

有兩種方式可以判斷物件內屬性，而其中的差別在於確認的<font color=#ee6e73>**屬性深度**</font>不同

### 方法一： obj.hasOwnProperty()

> obj.hasOwnProperty("key")

- key: 要判定的 key 值
- obj: 物件

```javascript
obj.hasOwnProperty("favorite");
//true

obj.hasOwnProperty("valueOf");
// false, valueOf 繼承自原型鏈結
```

### 方法二: in 運算子

> "key" in obj

- key: 要判定的 key 值
- obj: 物件

```javascript
"favorite" in obj;
//true

"valueOf" in obj;
// true
```

---

## <font color=#ee6e73> :herb: 差異</font>

hasOwnProperty() 只會檢查物件本身是否包含該屬性，而 in 運算子則會繼續往物件原型鏈 (Prototype chain) 上檢查。

在網頁 console 測試兩者差異

先建立物件
![建立物件](./assets/Javascript-ObjectHasKey/01.jpg)

展開物件後，可以看到除了我們設定的參數，還有 Prototype
![展開物件](./assets/Javascript-ObjectHasKey/02.jpg)

使用 hasOwnProperty() 和 in 運算子 來觀察其中差異。

發現因為 Prototype 裡有 `valueOf`，所以 in 運算子回傳的結果是 true，而 hasOwnProperty() 因為不會檢查 Prototype，所以回傳 false。
![觀察差異](./assets/Javascript-ObjectHasKey/03.jpg)

---

## <font color=#ee6e73> :herb: 參考資料</font>

- [How do I check if an object has a key in JavaScript? - Stack Overflow](https://stackoverflow.com/questions/455338/how-do-i-check-if-an-object-has-a-key-in-javascript)
- [檢查屬性是否存在物件內](https://www.jstips.co/zh_tw/javascript/check-if-a-property-is-in-a-object/)
- [繼承與原型鏈 - JavaScript | MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
- [重新認識 JavaScript: Day 04 物件、陣列以及型別判斷 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10190962)

---

cover: Photo by David van Dijk on [Unsplashn](https://unsplash.com/photos/3LTht2nxd34)
