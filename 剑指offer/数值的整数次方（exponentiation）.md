# 题目描述
给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

# 解法
本题还是对二进制的理解进行考察，主要用到的是快速幂的思想。将指数的值二进制化判断，然后乘上对应的次数，值得注意的是此题需要的指数（exponent）的正负进行判断，实现代码如下：
```java
public class Solution {
    public double Power(double base, int exponent) {
        //return Math.pow(base,exponent);
        double res = 1;
        int n;
        if(exponent == 0){
            return 1;
        }
        else{
            n = (exponent > 0) ? exponent : -exponent;
        }
        while(n != 0){
            res = ((n & 1) == 1)?res*base:res;
            base *= base;
            n >>= 1;
        }
        return (exponent > 0)?res:1/res;
  }
}
```
