## [15. 两数之和](https://leetcode-cn.com/problems/3sum/)
### 给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。

**注意：**:
### 答案中不可以包含重复的三元组。

**示例**:
```
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## ~~思路1~~: 暴力法：在两数相加的基础上多一层循环
### - 三层循环，时间复杂度O(n^3)

## 思路2: 双指针法：
### 1.先对数组排序；-时间复杂度O(nLog(n))
### 2.遍历数组(-时间复杂度O(n))，每次loop时在数组后续元素设置左右双指针，判断三数之和与0的大小来移动左右指针，向内夹逼(-时间复杂度O(n))
####    - 2.0 当前数字索引 = i，左指针left = i + 1， 右指针right = length - 1，3数之和sum = nums[i] +  nums[left] + nums[right]
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- 2.1 sum > 0时向左移动右指针
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- 2.2 sum < 0时向右移动左指针
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- 2.3 sum = 0时命中
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- 2.4 去重问题，因为数组已经排序，只看相邻元素即可，相邻元素重复时即使有解，也会与前面的重复元素相同，直接跳过即可。
### - 总体时间复杂度O(nLog(n)) + O(n) * O(n) = O(n ^ 2)

```
var threeSum = function(nums) {
    let result = [];

    // 1. 排序
    nums = nums.sort((a, b) => a - b);
    for (let i = 0; i < nums.length; i++) {
        let left = i + 1; // 左指针
        let right = nums.length - 1; // 右指针

        // 若最小的数 > 0，肯定不存在3数相加为0的情况
        if (nums[i] > 0) break;

        // 【去重】
        // 如果nums[i - 1]和nums[i]相同，即使有解也是重复解
        // 因为已排序过，所以去重只考虑相邻元素即可。
        if (i > 0 && (nums[i] == nums[i - 1])) continue;

        while (left < right) {
            let sum = nums[i] + nums[left] + nums[right];
            if (sum > 0) { // 2-1. 3数相加大于0时，向左移动右指针
                right--;
            } else if (sum < 0) { // 2-1. 3数相加小于0时，向右移动左指针
                left++;
            } else { // 2-3. 3数相加等于0时，找到目标，添加大result数组中
                result.push([nums[i], nums[left], nums[right]]);

                // 3. 向内移动双指针
                // 3-1. 先去重，相邻元素相等时，即使存在解也是重复解
                while (left < right && nums[left] == nums[left + 1]) {
                    left++; 
                }
                while (left < right && nums[right] == nums[right - 1]) {
                    right--;
                }

                // 3-1. 向内移动双指针各一步
                left++;
                right--;
            }
        }
    }
    return result;
};

console.log(threeSum([-1,0,1,2,-1,-4])); // [[-1,-1,2],[-1,0,1]]
```