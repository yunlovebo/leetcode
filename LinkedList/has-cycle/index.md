## [141. 给定一个链表，判断链表中是否有环。](https://leetcode-cn.com/problems/linked-list-cycle/)
### **此题需要看图，请点击官方题目链接**
### 为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。
### **你能用 O(1)（即，常量）内存解决此问题吗？**

**示例1**:
```
输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。
```

**示例2**:
```
输入：head = [1,2], pos = 0
输出：true
解释：链表中有一个环，其尾部连接到第一个节点。
```

**示例3**:
```
输入：head = [1], pos = -1
输出：false
解释：链表中没有环。
```

## 思路1: 哈希表
### 遍历链表，把节点存入一个hash表中，直到当前节点为null(无环)，或在hash表中找到当前节点(有环)。js中此法有多种变体。
### - 时间复杂度：O(n)
### - 空间复杂度：O(n)，不符合题目要求
```
var hasCycle = function(head) {
    let hash = {};
    while (head != null) {
        if (hash[head] !== undefined) {
            return true;
        } else {
            hash[head] = 1;
        }
        head = head.next;
    }

    return false;
};
```

## 思路2: 快慢指针
### - 快指针：1次移动2步。
### - 满指针：1次移动1步。
### - 循环终止条件1: 快指针移动到了null——无环
### - 循环终止条件2: 快慢指针相遇——有环
### - 时间复杂度：O(n)
### - 空间复杂度：O(1)

```
var hasCycle = function(head) {
    if (!head || !head.next) return false;

    let fast = head.next;
    let slow = head;

    while (fast != slow) {
        if (fast == null || fast.next == null) return false;
        fast = fast.next.next;
        slow = slow.next;
    }

    return true
};
```