---
title: LeetCode - Two sum
date: 2022-04-03 16:16:03
author: Hobby Lee
img: ./assets/Leetcode-twosum/cover.jpg
top: false
hide: false
cover: false
coverImg: ./assets/Leetcode-twosum/cover.jpg
summary: LeetCode 練習 - Two sum
categories: LeetCode
tags:
  - JavaScript
  - Array
  - Object
  - LeetCode
---

## <font color=#ee6e73> :herb: 難度：Easy </font>

---

## <font color=#ee6e73> :herb: 題目 </font>

給定一組擁有整數數字的陣列 (nums) 以及一個整數目標值 (target)，陣列中有兩個元素加起來會等於目標值 (target)，需將這兩個元素的索引值 (indices)，以陣列方式回傳

> Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

相同的元素不能重複使用，如 Example 3 的第一個 3 不能重複使用

> You may assume that each input would have exactly one solution, and you may not use the same element twice.

回傳的陣列值順序可任意排序

> You can return the answer in any order.

```
Example 1
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

```
Example2
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

```
Example3
Input: nums = [3,3], target = 6
Output: [0,1]
```

---

## <font color=#ee6e73> :herb: 初次解題</font>

- Runtime : 7652 ms
- Memory : 64.4 MB

第一次解題，花了一個小時左右才完成。用了兩個 find，中間跑迴圈時會有點搞不清楚現在跑到哪個值。不斷地用 console 確認後才終於解答。

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
  // 第一個索引值
  let first = "";

  // 第二個索引值
  let second = "";

  nums.find((item, key) => {
    // 將 nums 參考被到 temp
    let temp = JSON.parse(JSON.stringify(nums));

    // 計算 target 和 item 的差異
    let diff = target - item;

    // 將 key 值寫入第一個索引值
    first = key;

    // temp 陣列中，將當前元素值用 'x' 代替，避免重複使用元素
    temp.splice(key, 1, "x");

    // 在 temp 裡尋找與 diff 相等的元素，並將索引值寫入 second
    temp.find((j, index) => {
      if (j === diff) {
        second = index;
        return;
      }
    });
    return second;
  });

  return [first, second];
};
```

---

## <font color=#ee6e73> :herb: 進階解法</font>

- Runtime : 77 ms
- Memory : 42.4 MB

了解其他進階解法，發現用物件 (object) 解題的方法。一開始不太理解，也是嘗試印出 console 驗證，才逐步了解其中的邏輯。

利用物件沒有對應 key 值會回傳 <font color=#FF0000>**undefined**</font> 的特性，來判斷如果回傳 undefined，則將原本 nums 的元素當作 key，對應的索引值當作 value 寫入 map。在下一次的迴圈中再繼續判斷，直到有對應的 key 時才回傳陣列。

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
  var map = {};
  for (var i = 0; i < nums.length; i++) {
    var v = nums[i];

    console.log("map:", map);
    console.log("map[target - v]:", map[target - v]);

    if (map[target - v] >= 0) {
      return [map[target - v], i];
    } else {
      map[v] = i;
    }
  }
};
```

console.log 回傳結果測試

```javascript
nums: [2,7,11,15], target: 9

map: {}
map[target - v]: undefined

map: { '2': 0 }
map[target - v]: 0

---------------------------------
nums: [3,2,4], target: 6

map: {}
map[target - v]: undefined

map: { '3': 0 }
map[target - v]: undefined

map: { '2': 1, '3': 0 }
map[target - v]: 1

---------------------------------
nums: [3,2,4], target: 6

map: {}
map[target - v]: undefined

map: { '3': 0 }
map[target - v]: 0

```

---

## <font color=#ee6e73> :herb: 參考資料</font>

- [LeetCode-Two sum](https://leetcode.com/problemset/all/)
- [LeetCode with Javascript](https://skyyen999.gitbooks.io/-leetcode-with-javascript/content/questions/1md.html)

---

cover: Photo by <a href="https://unsplash.com/@twinsfisch?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Isabella and Zsa Fischer</a> on <a href="https://unsplash.com/s/photos/simple?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
