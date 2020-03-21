# 题目
Given a string, find the length of the longest substring without repeating characters.

# 解答
使用滑动窗口思想加hastset的结构去解答，实现代码如下：

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        //只用于保存子串内的字母
        HashSet<Character> set = new HashSet<Character>();
        int i = 0,j = 0,count = 0;
        while(i < s.length() && j < s.length()){
            if(!set.contains(s.charAt(j))){
                //不重复，加入
                set.add(s.charAt(j++));
                count = Math.max(count,j - i);
            }
            else{
                //重复移除set中的字母
                set.remove(s.charAt(i++));
            }
        }
        return count;
    }
}
```