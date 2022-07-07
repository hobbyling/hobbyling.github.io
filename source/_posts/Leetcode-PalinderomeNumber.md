---
title: Leetcode- Palinderome Number
tags:
  - JavaScript
  - Number
  - LeetCode
author: Hobby Lee
img: ./assets/Leetcode-PalinderomeNumber/cover.jpg
top: false
hide: false
cover: false
mathjax: true
coverImg: ./assets/Leetcode-PalinderomeNumber/cover.jpg
summary: LeetCode 練習 - Palinderome Number
categories: LeetCode
date: 2022-04-15 15:41:15
---


## <font color=#ee6e73> :herb: 難度：Easy </font>

---

## <font color=#ee6e73> :herb: 題目 </font>

給定一個整數 x，如果 x 是迴文數，則返回 true。

> Given an integer x, return true if x is palindrome integer.

迴文數的定義為：從前面讀和從後面讀是一樣的，是一個「對稱」的數
例如，121 是一個迴文數，而 123 不是

> An integer is a palindrome when it reads the same backward as forward.
> For example, 121 is a palindrome while 123 is not.

限制：$-2^{31}$ <= x <= $2^{31}$ - 1

> Constraints: $-2^{31}$ <= x <= $2^{31}$ - 1

更近一步：是否能在不將數字轉成字串的方式下解決問題呢？

> Follow up: Could you solve it without converting the integer to a string?

```
Example 1
Input: x = 121
Output: true

解釋：從左邊往右邊讀，和從右邊往左邊讀，都是 121
Explanation: 121 reads as 121 from left to right and from right to left.
```

```
Example 2
Input: x = -121
Output: false

解釋：從左邊往右邊讀是 -121，從右邊往左邊讀是 121-，所以不是迴文數
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

```
Example 3
Input: x = 10
Output: false

解釋：從左邊往右邊讀是 10，從右邊往左邊讀是 01，所以不是迴文數
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

---

## <font color=#ee6e73> :herb: 初次解題</font>

- Runtime : 167 ms
- Memory : 51.6 MB

第一次解題時，沒有注意到不要轉換成字串的提示，就滿心歡喜地轉換並解出答案。
先將數字拆解成陣列後，再進行比較

```javascript
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function (x) {
  // 將字串分解成陣列
  const arr = Array.from(x.toString());

  // 如果陣列第一個值是 '-'，則返回 false
  if (arr[0] === "-") return false;

  const len = arr.length;

  // 依序判斷前後值，若不相等，則返回 false
  for (let i = 0; i < len / 2; i++) {
    if (arr[i] !== arr[len - 1 - i]) return false;
  }

  return true;
};
```

轉換成字串的情況下，也可以直接反轉字串做比較

- Runtime : 195 ms
- Memory : 51.6 MB

```javascript
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function (x) {
  return x == x.toString().split("").reverse().join("");
};
```

---

## <font color=#ee6e73> :herb: 不使用字串</font>

- Runtime : 904 ms
- Memory : 57.8 MB

了解其他進階解法，是用取餘數和整數的方式處理。

- %：回傳剩下的餘數，ex 15 % 10 = 5
- Math.floor(): 回傳小於等於所給數字的最大整數，ex Math.floor(5.09) => 5

先判斷數字：

- 負數：一定不是迴文數
- 個位數：一定是迴文數

```javascript
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function (x) {
  // 若為負數，則返回 false
  if (x < 0) return false;

  // 若為個位數，則返回 true
  if (x < 10) return true;

  // 算出 x 是幾位數
  let digits = 1;
  while (x / digits >= 10) {
    digits *= 10;
  }

  while (x > 0) {
    // 取第一個數字
    let first = Math.floor(x / digits);

    // 取最後一個數字
    let last = x % 10;

    if (first !== last) return false;

    // 去除頭尾後繼續比對
    console.log("x:", x);
    console.log("x % digits:", x % digits);
    console.log("(x % digits) / 10:", (x % digits) / 10);
    console.log(
      "Math.floor((x % digits) / 10))",
      Math.floor((x % digits) / 10)
    );

    x = Math.floor((x % digits) / 10);

    // 因為比完頭尾所以少了兩位數 / 100
    digits = digits / 100;
  }
  return true;
};
```

console.log 回傳結果測試

```javascript
input: 121

x: 121
x % digits: 21
(x % digits) / 10: 2.1
Math.floor((x % digits) / 10)): 2

x: 2
x % digits: 0
(x % digits) / 10: 0
Math.floor((x % digits) / 10)): 0

---
input: 123141

x: 123141
x % digits: 23141
(x % digits) / 10: 2314.1
Math.floor((x % digits) / 10)): 2314
```

---

## <font color=#ee6e73> :herb: 參考資料</font>

- [LeetCode-Palindrome Number](https://leetcode.com/problems/palindrome-number/)
- [LeetCode Note](https://hannahpun.gitbook.io/leetcode-note/math/9-palindrome-number)

---

cover: Photo by <a href="https://unsplash.com/@sarahdorweiler?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Sarah Dorweiler</a> on <a href="https://unsplash.com/s/photos/flower?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
