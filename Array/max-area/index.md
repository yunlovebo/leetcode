## [11. 盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)
### 给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

**示例**:
```
输入: [1,8,6,2,5,4,8,3,7]
输出: 49
```

![示例图片](https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/07/25/question_11.jpg)

**说明**:
### 你不能倾斜容器，且 n 的值至少为 2。

## ~~思路1~~: 暴力法：简单地考虑每对可能出现的线段组合并找出这些情况之下的最大面积。
### - 双层循环，时间复杂度O(n^2)

## 思路2: 双指针法：两线段之间的面积取决于较短险段，两线段距离越远，得到的面积就越大，所以每次移动较短的线段，并且移动后的线段比之前的更长才去计算面积，直到两个指针相遇，保留面积最大值。
### - 一层循环，时间复杂度O(n)


```
var maxArea = function(height) {
    let result = 0;
    let i = 0; 
    let j = height.length - 1;
    let lasti = 0; // 保存上一次左侧高度
    let lastj = 0; // 保存上一次右侧高度
    
    while (i < j) {
        if (height[i] < height[j]) {
            if (height[i] > lasti) { // 如果移动后左侧的高度小于等于上一次左侧高度，本次面积肯定没有上次大，无需计算
                result = Math.max(result, height[i] * (j - i));
            }
            lasti = height[i];
            i++;
        } else {
            if (height[j] > lastj) { // 右侧同理
                result = Math.max(result, height[j] * (j - i));
            }
            lastj = height[j];
            j--;
        }
    }
    

    return result;
};

console.log(maxArea([1,8,6,2,5,4,8,3,7])); // 49
```