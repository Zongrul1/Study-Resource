# 题目
有两个用链表表示的整数，每个结点包含一个数位。这些数位是反向存放的，也就是**个位排在链表的首部**。编写函数对这两个整数求和，并用链表形式返回结果。

给定两个链表ListNode* A，ListNode* B，请返回A+B的结果(ListNode*)。

测试样例：

> {1,2,3},{3,2,1}
返回：{4,4,4}

# 解答
本题由于是反向存放，所以省了不少事，可以顺序计算，但是要注意进位的问题，和链表的进位的问题，具体代码实现为下：

```java
import java.util.*;
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Plus {
    public ListNode plusAB(ListNode a, ListNode b) {
        // write code here
        ListNode d = new ListNode(0);//头节点
        ListNode c = d;
        int sum,j = 0,i = 0;
        while(a != null||b != null||j != 0){//将进位的最后一位置于末位
        	//如果节点为空，值置为0
            int aVal = a != null ? a.val : 0;
            int bVal = b != null ? b.val : 0;
            sum = aVal + bVal + j;
            i = sum%10;//余数
            j = sum/10;//进位
            c.next = new ListNode(i);//插入余数
            c = c.next;
            //进位
            a = a != null ? a.next : null;
            b = b != null ? b.next : null;
        }
        return d.next;//输出初始节点的下一个点
    }
}
```
