# 题目描述
输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

# 解答
利用滑动窗口解决，而且第一个得到的答案必定为最小，代码实现如下：
```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> FindNumbersWithSum(int [] array,int sum) {
        int i = 0;
        int j = array.length - 1;
        ArrayList<Integer> A = new ArrayList<Integer>();
        if(array.length == 0){
            return A;
        }
        while(i < j){
            if(array[i] + array[j] == sum){
                A.add(array[i]);
                A.add(array[j]);
                return A;
            }
            else if(array[i] + array[j] < sum){
                i++;
            }
            else if(array[i] + array[j] > sum){
                j--;
            }            
        }
        return A;
    }
}
```
