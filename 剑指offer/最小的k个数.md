# 题目描述
输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

# 解法1
递归，复杂度高
```java
import java.util.*;
public class Solution {
    ArrayList<Integer> A = new ArrayList<Integer>();
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        if(k > input.length){
            return A;
        }
        if(k == 0){
            return A;
        }
        else{
            int min = input[0];
            int j = 0;
            for(int i = 1;i < input.length;i++){
                if(input[i] < min){
                    min = input[i];
                    j = i;
                }
            }
            A.add(min);
            input[j] = 9999;
            GetLeastNumbers_Solution(input,k - 1);
            return A;
        }
    }
}
```
# 解法2
预处理 O（n），实际上O（nlogn）以上
```java
import java.util.*;
public class Solution {
    ArrayList<Integer> A = new ArrayList<Integer>();
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        if(k > input.length){
            return A;
        }    
        if(input == null){
            return A;
        }
        Arrays.sort(input);
        for(int i = 0;i < k;i++){
            A.add(input[i]);
        }
        return A;
    }
}
```
# 解法3
优先队列，用最大堆保存这k个数，每次只和堆顶比，如果比堆顶小，删除堆顶，新数入堆。比较巧妙的一种方法。
```java
import java.util.ArrayList;
import java.util.PriorityQueue;
import java.util.Comparator;
public class Solution {
   public ArrayList<Integer> GetLeastNumbers_Solution(int[] input, int k) {
       ArrayList<Integer> result = new ArrayList<Integer>();
       int length = input.length;
       if(k > length || k == 0){
           return result;
       }
        PriorityQueue<Integer> maxHeap = new PriorityQueue<Integer>(k, new Comparator<Integer>() {
 
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2.compareTo(o1);
            }
        });
        for (int i = 0; i < length; i++) {
            if (maxHeap.size() != k) {
                maxHeap.offer(input[i]);
            } else if (maxHeap.peek() > input[i]) {
                Integer temp = maxHeap.poll();
                temp = null;
                maxHeap.offer(input[i]);
            }
        }
        for (Integer integer : maxHeap) {
            result.add(integer);
        }
        return result;
    }
}
```
