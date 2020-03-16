# 题目
请编写一个方法，找出两个数字中最大的那个。条件是不得使用if-else等比较和判断运算符。
给定两个int a和b，请返回较大的一个数。若两数相同则返回任意一个。

# 解答
方法1：数组排序
```javascript
import java.util.*;

public class Max {
    public int getMax(int a, int b) {
        // write code here
        int[] A = {a,b};
        Arrays.sort(A);
        return A[1];
    }
}
```

方法2：数学公式
```javascript
import java.util.*;

public class Max {
    public int getMax(int a, int b) {
        return((a + b + abs(a - b)) / 2);
        // write code here
    }
};
```