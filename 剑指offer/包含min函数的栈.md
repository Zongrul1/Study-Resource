# 题目描述
定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

# 解法
使用两个栈去完成，一个正常使用，一个用来存放每次入栈的最小值，当需要出栈的同时，则两个栈同时出栈，以此完成一个同步的存放最小值的结构，实现代码如下：

```java
import java.util.Stack;

public class Solution {
    private Stack<Integer> S1 = new Stack<Integer>();
    private Stack<Integer> S2 = new Stack<Integer>();    
    private int min = Integer.MAX_VALUE;
    public void push(int node) {
        S1.push(node);
        if(node < min){
            min = node;
        }
        S2.push(min);
    }
    
    public void pop() {
        S1.pop();
        S2.pop();
    }
    
    public int top() {
        return S1.peek();
    }
    
    public int min() {
        return S2.peek();
    }
}
```
