## [24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)
### 给定一个链表，两两交换其中相邻的节点，并返回交换后的链表
### **你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。**

**示例**:
```
给定 1->2->3->4, 你应该返回 2->1->4->3.
```

## 思路1: 迭代：需要temp缓存上次head的指向。
### - 时间复杂度：O(n)
### - 空间复杂度：O(1)
```
var swapPairs = function (head) {
    let thead = new ListNode(0);
    thead.next = head;
    let tmp = thead;
    while(tmp.next != null && tmp.next.next != null){
        let start = tmp.next;
        let end = start.next;
        tmp.next = end;
        start.next = end.next;
        end.next = start;
        tmp = start;
    }
    return thead.next;
}
```

## 思路2: 递归：非0元素依次拷贝进新数组，最后用0补齐。[个人感觉此题递归法比迭代法更容易理解]
### - (1)终止条件：head == null(链表为空)、head.next == null(只有一个元素)。
### - (2)递归步骤：交换head和next(next为已处理好的子链表)，返回交换完的子链表。
### - 时间复杂度：O(n)
### - 空间复杂度：O(n)


```
var swapPairs = function(head) {
    if (head == null || head.next == null) return head;
    let next = head.next;
    head.next = swapPairs(next.next);
    next.next = head;
    return next;
};
```