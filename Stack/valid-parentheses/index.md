## [20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)
### 给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

**说明**:
### 这个比较常见了

## ~~思路1~~: 暴力法：遍历字符串，去掉成对出现的括号，最后检查字符串是否为空
### - 因为比较常见的栈方法先入为主，这种方法反而不容易想到T_T，代码暂时省略
### 时间复杂度：O(n^2)
### 空间复杂度：O(n)

## 思路2: 栈：这种就近匹配的问题一般会考虑用到栈。
### - 遇到左括号入栈，遇到右括号出栈，检查是否匹配，不匹配立即返回false(右括号错误)，遍历后栈不为空返回false(左括号错误)；
### - 左右括号建立hash关系，将左括号对应的右括号入栈，检查相等时可以直接比较，节省时间。
### 时间复杂度：O(n) (一遍循环)
### 空间复杂度：O(n) (hash表和栈使用的线性空间)

```
var isValid = function(s) {
    let stack = [];

    let hash = {
        '(': ')',
        '[': ']',
        '{': '}',
    };

    for (let i = 0; i < s.length; i++) {
        let cur = s.slice(i, i+1);
        if (hash[cur]) {
            stack.push(hash[cur]);
        } else {
            if (cur === stack[stack.length - 1]) {
                stack.pop();
            } else {
                return false;
            }
            
        }
    }

    return stack.length === 0;
};
```