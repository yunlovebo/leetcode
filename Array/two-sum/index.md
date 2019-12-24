## [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)
### 给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

### 你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

**示例**:
```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

## ~~思路1~~: 暴力法：遍历每个元素x，并查找是否存在一个目标元素与target - x相等。
### - 两层循环，时间复杂度O(n^2)

## 思路2: 两遍哈希表：先把迭代数组到一个map里，用空间换时间，查找元素的时间复杂度从O(n)下降到O(1)；第二次迭代时检查当前元素x对应的target - x 是否在map中。
### - 两次一层循环，时间复杂度O(n)

## 思路3: 一遍哈希表：与两遍哈希表类似，迭代数组到map中的同时，检查map中是否已存在当前元素x对应的target - x
### - 一层循环，时间复杂度O(n)



***以下代码实现的是思路3，一遍哈希表***
```
var twoSum = function(nums, target) {
    let result = [];
    let map = {}; // js中的json对象就是map

    nums.forEach((element, index) => {
        if (map[target - element] !== undefined) {
            result = [map[target - element], index];
        }
        map[element] = index;
    });

    return result;
};

console.log(twoSum([2,7,11,15], 9)); // [0, 1]
```