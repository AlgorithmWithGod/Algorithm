```java
import java.io.*;
import java.util.*;

class Solution
{
    public int solution(int n, int a, int b)
    {
        int answer = 0;
        a--;
        b--;
        while (a != b){
            answer++;
            a /= 2;
            b /= 2;
        }

        return answer;
    }
}
```
