```java
import java.util.*;
class Solution
{
    public int solution(int []A, int []B)
    {
        int answer = 0;
        
        Arrays.sort(A);
        Arrays.sort(B);
        
        int Aidx = 0;
        int Bidx = B.length-1;
        
        for(int i = 0; i<A.length; i++){
            answer += (A[Aidx++]*B[Bidx--]);
        }

        return answer;
    }
}
```
