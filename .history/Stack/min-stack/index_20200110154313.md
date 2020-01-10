## [20. 最小栈](https://leetcode-cn.com/problems/min-stack/)
### · push(x) -- 将元素 x 推入栈中。
### · pop() -- 删除栈顶的元素。
### · top() -- 获取栈顶元素。
### · getMin() -- 检索栈中的最小元素。

**示例**:
```
    MinStack minStack = new MinStack();
    minStack.push(-2);
    minStack.push(0);
    minStack.push(-3);
    minStack.getMin();   --> 返回 -3.
    minStack.pop();
    minStack.top();      --> 返回 0.
    minStack.getMin();   --> 返回 -2.
```

## 思路: 用一个辅助栈helper，stack栈正常保存数据
### - push时，如果将入栈元素x <= helper.peek，则同时压入helper 和 stack，这样就可以保证helper里保存的是当前最小值；
### - pop时，如果 helper 和 stack 的栈顶元素相同，则同时出栈，否则只有stack出栈；
### - getMin时取helper栈顶元素。
### 时间复杂度：O(1) (栈的特性)
### 空间复杂度：O(n) 

```
    /**
    * initialize your data structure here.
    */
    var MinStack = function() {
        this.stack = [];
        this.helper = []; // 压入最小值
    };

    /** 
    * x <= helpeer.peek时压入helper，否则不压入helper
    * @param {number} x
    * @return {void}
    */
    MinStack.prototype.push = function(x) {
        this.stack.push(x);
        if (this.helper.length == 0 || this.helper[this.helper.length - 1] >= x) { // 处理边界情况
            this.helper.push(x);
        }
    };

    /**
    * @return {void}
    */
    MinStack.prototype.pop = function() {
        if (this.stack.length < 0) return 0;
        if (this.stack[this.stack.length - 1] == this.helper[this.helper.length - 1]) {
            this.helper.pop();
        }
        this.stack.pop();
    };

    /**
    * @return {number}
    */
    MinStack.prototype.top = function() {
        if (this.stack.length == 0) return 0;
        return this.stack[this.stack.length - 1];
    };

    /**
    * @return {number}
    */
    MinStack.prototype.getMin = function() {
        if (this.helper.length == 0) return 0;
        return this.helper[this.helper.length - 1];
    };
```