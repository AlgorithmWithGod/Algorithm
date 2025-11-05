```java
import java.util.*;

class Solution {
    public int solution(int[] priorities, int location) {
        int[] cnt = new int[10];
        for (int p : priorities) cnt[p]++;

        ArrayDeque<int[]> q = new ArrayDeque<>();
        for (int i = 0; i < priorities.length; i++) q.offer(new int[]{priorities[i], i});

        int cur = 9;
        while (cur > 0 && cnt[cur] == 0) cur--;

        int order = 0;
        while (!q.isEmpty()) {
            int[] doc = q.poll();
            int p = doc[0], idx = doc[1];

            if (p == cur) {
                order++;
                cnt[p]--;
                if (idx == location) return order;
                while (cur > 0 && cnt[cur] == 0) cur--;
            } else { 
                q.offer(doc);
            }
        }
        return -1;
    }
}

```
