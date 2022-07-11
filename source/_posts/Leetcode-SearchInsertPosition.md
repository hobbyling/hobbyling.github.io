---
title: LeetCode - Search Insert Position
tags:
  - JavaScript
  - Array
  - Binary Search
  - LeetCode
author: Hobby Lee
img: ./assets/Leetcode-SearchInsertPosition/cover.jpg
top: false
hide: false
cover: false
mathjax: true
coverImg: ./assets/Leetcode-SearchInsertPosition/cover.jpg
summary: LeetCode 練習 - Search Insert Position
categories: LeetCode
date: 2022-06-14 11:00:03
---


## <font color=#ee6e73> :herb: 難度：Easy </font>

---

## <font color=#ee6e73> :herb: 題目 </font>
給定一組由不同整數組成的陣列以及一個目標值，若在陣列內找到目標值，則返回索引。若在陣列內找不到目標值，則返回該目標值插入陣列並排序後的索引。
> Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

您必須編寫一個具有 O(log n) 運行時復雜度的算法。
> You must write an algorithm with O(log n) runtime complexity.

限制
- 1 <= 陣列長度 <= $10^{4}$
- -$10^{4}$ <= 陣列內的單一值 <= $10^{4}$
- 陣列內包含按照升序排序的不同值
- -$10^{4}$ <= 目標值 <= $10^{4}$
> Constraints:
> 1 <= nums.length <= $10^{4}$
> -$10^{4}$ <= nums[i] <= $10^{4}$
> nums contains distinct values sorted in ascending order.
> -$10^{4}$ <= target <= $10^{4}$

```
Example 1:

Input: nums = [1,3,5,6], target = 5
Output: 2
```

```
Example 2:

Input: nums = [1,3,5,6], target = 2
Output: 1
```

```
Example 3:

Input: nums = [1,3,5,6], target = 7
Output: 4
```

---

## <font color=#ee6e73> :herb: 解題</font>

### 解法：Array

- Runtime : 62 ms
- Memory : 41.8 MB

使用 indexOf 尋找 target 是否存在 nums 內，
- 若有，則回傳索引
- 若沒有，則把 target push 入 nums，排序的值後再用 indexOf 找出索引

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {法
    let idx = nums.indexOf(target)
    
    if (idx < 0) {
        nums.push(target)
        nums.sort((a, b) => a-b)
        return nums.indexOf(target)
    } else {
        return idx
    }
};
```

### 解法：Binary search

- Runtime : 97 ms
- Memory : 42.4 MB

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
    let start = 0
    let end = nums.length -1
    
    while(start <= end) {
        let mid = start + Math.floor((end-start)/2)
        
        if(nums[mid] === target) {
            return mid
        } else if(nums[mid] > target) {
            end = mid -1
        } else {
            start = mid +1
        }
    }
    
    return start
};
```

---

## <font color=#ee6e73> :herb: 參考資料</font>
- [LeetCode - 35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)

---

cover: Photo by <a href="https://unsplash.com/photos/oppYzALtH88">Evie S.</a> on <a href="https://unsplash.com/s/photos/plant?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>