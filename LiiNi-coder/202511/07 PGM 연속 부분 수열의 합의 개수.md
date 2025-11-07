```java
import java.util.*;

class Solution {
    public int solution(int[] elements) {
        int length = elements.length;
        int[] arr = new int[length * 2];
        for(int i = 0; i < length * 2; i++){
            arr[i] = elements[i % length];
        }
        Set<Integer> set = new HashSet<>();
        for(int size = 1; size <= length; size++){
            for(int start = 0; start < length; start++){
                int sum = 0;
                for(int i = start; i < start + size; i++){
                    sum += arr[i];
                }
                set.add(sum);
            }
        }

        return set.size();
    }
}

```
