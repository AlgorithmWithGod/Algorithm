```java
import java.util.*;

class Solution {
    public int solution(String[][] clothes) {
        Map<String, Integer> countByType = new HashMap<>();
        for (String[] cloth : clothes) {
            String type = cloth[1];
            countByType.put(type, countByType.getOrDefault(type, 0) + 1);
        }
        int combinations = 1;
        for (int count : countByType.values()) {
            combinations *= (count + 1);
        }
        combinations -= 1;

        return combinations;
    }
}

```
