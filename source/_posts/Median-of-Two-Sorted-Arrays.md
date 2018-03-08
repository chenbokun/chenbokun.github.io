---
title: 两个有序数组和的中位数
date: 2017-12-17 11:28:27
tags: [Array]
categories: LeetCode
---

拿到这道题想了很久，以我最初的想法去做有太多的可变性了，导致不得不在代码中书写N多的if else，但结果还好，计算了188ms，在时间复杂度和空间占用率上都排到了前10%，文章中对第一位162ms的解题思想做了记录。
<!--more-->
## 题示

![Question in here](/images/mtsa-q.png)
链接: [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)

## 想法

如果是一个有序数组，我们很自然的会根据数组长度的奇偶来取得中位数，而两个有序数组的思想同上。我们只需要依次从两个数组中取数，每次取小的那位，一直取到totalLength>>>2 + 1,在循环中每次保存前一位数(x)和当前数(y)，循环完成后，判断totalLength的奇偶，即可得到结果为y或者(x+y)/2

## 解决方案

``` JavaScript
var findMedianSortedArrays = function(nums1, nums2) {
    let sumLen = nums1.length + nums2.length;
    let targetLen = sumLen >>> 1;
    let loop = targetLen + 1;
    let i = 0;
    let j = 0;
    let x, y;

    while (loop--) {
        x = y;
        if (nums1[i] === undefined) {
            y = nums2[j++]
        } else if (nums2[j] === undefined) {
            y = nums1[i++];
        } else if (nums1[i] < nums2[j]) {
            y = nums1[i++];
        } else {
            y = nums2[j++];
        }
    }

    return targetLen << 1 === sumLen ? (x + y) / 2 : y;
};
```
