```java
import java.util.*;
class Solution {
    public int[] solution(int[] sequence, int k) {
        List<int[]> list = new ArrayList<>();
        int start = 0, end = 0, sum = sequence[0];
        while (start < sequence.length && end < sequence.length) {
            if (sum == k) {
                list.add(new int[] {start, end});
            }
            if (sum <= k) {
                end++;
                if (end < sequence.length)
                    sum += sequence[end];
            } else {
                if (start < sequence.length)
                    sum -= sequence[start];
                start++;
            }
        }
        Collections.sort(list, new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                int len1 = o1[1] - o1[0];
                int len2 = o2[1] - o2[0];
                return len1 - len2;
            }
        });
        int[] answer = {list.get(0)[0], list.get(0)[1]};
        return answer;
    }
}
```
