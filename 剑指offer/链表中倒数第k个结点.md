# 题目描述
输入一个链表，输出该链表中倒数第k个结点。

# 解法
思路1：
利用栈的特性解决，值得注意的是几种特殊情况，需要进行过滤判断

 1. 链表为空
 2. k为0
 3. k比链表元素个数多

实现代码如下：
```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
import java.util.Stack;
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        if(head == null){
            return null;
        }
        else if(k == 0){
            return null;
        }
        Stack<ListNode> s = new Stack<ListNode>();
        int count = 0;
        while(head != null){
            s.push(head);   
            head = head.next;
            count++;
        }
        if(count < k){
            return null;
        }
        while(k > 1){
            s.pop();
            k--;
        }
        return s.pop();
    }
}
```
思路2：
采用快慢指针的方法，让一快指针先走k步，然后两指针再同时出发，当快指针到头时，返回慢指针即可，实现代码如下：

```java
public ListNode FindKthToTail(ListNode head,int k) { //5,{1,2,3,4,5}
        ListNode p, q;
        p = q = head;
        int i = 0;
        for (; p != null; i++) {
            if (i >= k)
                q = q.next;
            p = p.next;
        }
        return i < k ? null : q;
    }
```
