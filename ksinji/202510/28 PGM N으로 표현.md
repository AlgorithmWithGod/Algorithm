```java
import java.util.*;
 
class Solution {
    public int solution(int N, int number) {
        if (N == number) {
            return 1;
        }
 
        List<Set<Integer>> num = new ArrayList<>();
        for (int i = 0; i <= 8; i++) {
            num.add(new HashSet<>());
        }
 
        num.get(1).add(N);
 
        for (int i = 2; i <= 8; i++) {
            StringBuilder sb = new StringBuilder().append(N);
            for (int j = 1; j < i; j++) {
                sb.append(N);
            }
            num.get(i).add(Integer.parseInt(sb.toString()));
            
            for (int j = 1; j < i; j++) {
                int k = i - j;
                for (int num1 : num.get(j)) {
                    for (int num2 : num.get(k)) {
                        num.get(i).add(num1 + num2);
                        num.get(i).add(num1 - num2);
                        num.get(i).add(num1 * num2);
                        if (num2 != 0) {
                            num.get(i).add(num1 / num2);
                        }
                    }
                }
            }
 
            if (num.get(i).contains(number)) {
                return i;
            }
        }
 
        return -1;
    }
}
```
