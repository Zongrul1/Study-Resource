```java
public class test {
    public static void main(String[] args) {
        int x = 2;
        double left = 0,right = x,mid;
        if (right < 1) {
            right = 1;
        }
        while (left + 1e-12 < right) {
            mid = left + (right - left) / 2;
            if (mid * mid < x) {
                left = mid;
            }
            else{
                right = mid;
            }
        }
        System.out.println(left);
    }
}
```