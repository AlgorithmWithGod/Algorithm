```java
import java.util.*;

class Solution
{
    public int solution(int []A, int []B)
    {
        int answer = 0;
        List<Integer> a = new ArrayList<>();
        for(int i: A){
            a.add(i);
        }
        List<Integer> b = new ArrayList<>();
        for(int i: B){
            b.add(i);
        }
        Collections.sort(a);
        Collections.sort(b, Collections.reverseOrder());
        for(int i = 0; i<A.length; i++)
            answer += a.get(i)*b.get(i);


        return answer;
    }
}
```
