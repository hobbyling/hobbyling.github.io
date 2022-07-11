---
title: Leetcode-Guess Number Higher Or Lower
tags:
  - JavaScript
  - Binary Search
  - LeetCode
author: Hobby Lee
img: ./assets/Leetcode-GuessNumberHigherOrLower/cover.jpg
top: false
hide: false
cover: false
mathjax: true
coverImg: ./assets/Leetcode-GuessNumberHigherOrLower/cover.jpg
summary: LeetCode 練習 - Guess Number Higher Or Lower
categories: LeetCode
date: 2022-06-13 11:07:00
---


## <font color=#ee6e73> :herb: 難度：Easy </font>

---

## <font color=#ee6e73> :herb: 題目 </font>

我們正在玩猜數字遊戲，規則如下:
> We are playing the Guess Game. The game is as follows:

我在 1 到 n 中選定一個數字，你必須猜中我所指定的數字。
每當你猜錯時，我將告訴你，你猜的數字比指定數字高還是低。
> I pick a number from 1 to n. You have to guess which number I picked.
> Every time you guess wrong, I will tell you whether the number I picked is higher or lower than your guess.

你將呼叫一個預定義的整數猜測 API（整數），此 API 會回傳三種結果
- -1: 你猜的數字高於指定數字
- 1: 你猜的數字低於指定數字
- 0: 你猜的數字等於指定數字

> You call a pre-defined API int guess(int num), which returns three possible results:
> -1: Your guess is higher than the number I picked (i.e. num > pick).
> 1: Your guess is lower than the number I picked (i.e. num < pick).
> 0: your guess is equal to the number I picked (i.e. num == pick).

最後回傳指定數字
> Return the number that I picked.

限制：
- 1 <= n <= $2^{31}$ - 1
- 1 <= pick <= n

> Constraints: 
> 1 <= n <= $2^{31}$ - 1
> 1 <= pick <= n

```
Example 1:

Input: n = 10, pick = 6
Output: 6
```

```
Example 2:

Input: n = 1, pick = 1
Output: 1
```

```
Example 3:

Input: n = 2, pick = 1
Output: 1
```

## <font color=#ee6e73> :herb: 解題</font>

```javascript
/** 
 * Forward declaration of guess API.
 * @param {number} num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * var guess = function(num) {}
 */

/**
 * @param {number} n
 * @return {number}
 */
var guessNumber = function(n) {
    let start = 1;
    let end = n;
    
    while(start <= end) {
        let mid = start + Math.floor((end-start)/2)
        
        if (guess(mid) === 0){
            return mid
        } else if(guess(mid) === 1) {
            start = mid+1
        } else {
            end = mid-1
        }
    }
};
```

---

## <font color=#ee6e73> :herb: 參考資料</font>
- [LeetCode - 374. Guess Number Higher or Lower](https://leetcode.com/problems/guess-number-higher-or-lower/)

---

cover: Photo by <a href="https://unsplash.com/photos/8ioenvmof-I">Jazmin Quaynor</a> on <a href="https://unsplash.com/s/photos/flower?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>