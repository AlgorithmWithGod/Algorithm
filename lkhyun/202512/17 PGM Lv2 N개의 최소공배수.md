```java
import java.util.*;
class Solution {
    public int solution(int[] arr) {
        int lcm = arr[0];
        for(int i = 1; i<arr.length; i++){
            lcm = LCM(lcm,arr[i]);
        }
        return lcm;
    }
    public int GCD(int a, int b) {return b == 0 ? a : GCD(b, a%b);}
    public int LCM(int a, int b) {return (a*b) / GCD(a,b);}
    
}
```
