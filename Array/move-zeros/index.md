## [283. 移动零](https://leetcode-cn.com/problems/move-zeroes/)
### 给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

**示例**:
```
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```

**说明**:
### 1. 必须在原数组上操作，不能拷贝额外的数组。
### 2. 尽量减少操作次数。

## ~~思路1~~: 暴力法：循环数组，删除为0元素，记录0的个数，最后在数组末尾补齐。
### - 缺点：删除数组元素需频繁操作

## ~~思路2~~: 创建新数组：非0元素依次拷贝进新数组，最后用0补齐。
### - 不满足题设，需要拷贝额外的数组。

## 思路3: 双指针：一个指针i遍历数组，另一个指针index标记非0元素应该插入的位置，其原位置补0，相当于0与非0元素交换。
### - 不创建新数组，一层循环时间复杂度O(n)


```
function moveZeros (nums) {
    if (nums.length == 0) return [];
    let index = 0; // 非0元素放置的位置
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] != 0) {
            nums[index] = nums[i];
            if (index != i) {
                nums[i] = 0;
            }
            index++;
        }
    }
    return nums;
}

console.log(moveZeros([0,1,0,3,12])); // [1, 3, 12, 0, 0]
```