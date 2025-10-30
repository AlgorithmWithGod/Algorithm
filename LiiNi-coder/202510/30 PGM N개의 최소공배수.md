```java
import java.util.*;

class Solution {
    public int solution(int[] arr) {
        long lcm = arr[0];
        for(int i=1; i<arr.length; i++){
            lcm = lcm(lcm, arr[i]);
        }
        return (int)lcm;
    }
    private static long gcd(long a, long b){
        while(b != 0){
            long t = a % b;
            a = b;
            b = t;
        }
        return a;
    }
    private static long lcm(long a, long b){
        return (a / gcd(a, b)) * b;
    }
}

```
