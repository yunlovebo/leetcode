## [84. 柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)
### 给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。
### 求在该柱状图中，能够勾勒出来的矩形的最大面积。


**示例(去官网上看图)**:
```
    输入: [2,1,5,6,2,3]
    输出: 10
```

## ~~思路1~~: 暴力法：3重循环求出每个包含当前柱的面积
### (太暴力了，代码略)
### 时间复杂度：O(n^3)
### 空间复杂度：O(1) 

## 思路2: 栈解
### 1. 在左右两侧各增加一个为高度0的柱
### 2. 遍历柱状图，每个柱左侧第一个比高度自己小和右侧第一个高度比自己小的柱子中间围起来的面积就是包含当前柱子的矩形面积;
### 3.1. 若stack为空或者当前柱子高度大于前一项，则将当前柱子的index压入到stack.
### 3.2. 否则将stack的栈顶元素出栈
### 时间复杂度：O(n)
### 空间复杂度：O(n) 

```
    var largestRectangleArea = function(heights) {
        let maxArea = 0;

        let stack = [];
        
        heights.push(0);
        heights.unshift(0);

        for (let i = 0; i < heights.length; i++) {
            while (stack.length > 0 && heights[stack[stack.length - 1]] > heights[i]) {
                let curArea =  heights[stack.pop()] * (i - stack[stack.length - 1] - 1);
                maxArea = Math.max(maxArea, curArea);
            }
            stack.push(i);
        }

        return maxArea;
    };
```