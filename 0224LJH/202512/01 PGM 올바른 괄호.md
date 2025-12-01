```java
import java.io.*;
import java.util.*; 

class Solution {
    boolean solution(String s) {
        boolean answer = true;
        char[] arr = s.toCharArray();
        int cur = 0;
        
        for (int i = 0; i < arr.length; i++){
            cur += (arr[i] == '(')?1:-1;
            if (cur < 0 ) return false;
        }
        if (cur != 0) return false;


        return true;
    }
}
```
