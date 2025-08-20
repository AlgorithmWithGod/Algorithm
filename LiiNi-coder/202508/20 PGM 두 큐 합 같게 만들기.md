```java
import java.util.*;

class Solution {
    static class BfsQElement {
        int count;
        ArrayDeque<Integer> q1;
        ArrayDeque<Integer> q2;
        long sum1;
        long sum2;

        BfsQElement(int count, ArrayDeque<Integer> q1, ArrayDeque<Integer> q2, long sum1, long sum2) {
            this.count = count;
            this.q1 = q1;
            this.q2 = q2;
            this.sum1 = sum1;
            this.sum2 = sum2;
        }
    }

    public int solution(int[] queue1, int[] queue2) {
        long total = 0;
        long sum1 = 0, sum2 = 0;

        var q1 = new ArrayDeque<Integer>();
        var q2 = new ArrayDeque<Integer>();

        for (int i : queue1) {
            q1.offer(i);
            sum1 += i;
            total += i;
        }
        for (int i : queue2) {
            q2.offer(i);
            sum2 += i;
            total += i;
        }
        if (total % 2 != 0)
          return -1;
        long target = total / 2;
        var bfsQ = new ArrayDeque<BfsQElement>();
        bfsQ.offer(new BfsQElement(0, q1, q2, sum1, sum2));
        
        Set<String> visited = new HashSet<>();//방문상태
        visited.add(sum1 + "," + sum2);

        while (!bfsQ.isEmpty()) {
            BfsQElement cur = bfsQ.poll();

            if (cur.sum1 == target) {
                return cur.count;
            }

            if (!cur.q1.isEmpty()) {
                int val = cur.q1.peek();
                var newQ1 = new ArrayDeque<>(cur.q1);
                var newQ2 = new ArrayDeque<>(cur.q2);
                newQ1.poll();
                newQ2.offer(val);

                long newSum1 = cur.sum1 - val;
                long newSum2 = cur.sum2 + val;
                String key = newSum1 + "," + newSum2;

                if (!visited.contains(key)) {
                    visited.add(key);
                    bfsQ.offer(new BfsQElement(cur.count + 1, newQ1, newQ2, newSum1, newSum2));
                }
            }

            if (!cur.q2.isEmpty()) {
                int val = cur.q2.peek();
                var newQ1 = new ArrayDeque<>(cur.q1);
                var newQ2 = new ArrayDeque<>(cur.q2);
                newQ2.poll();
                newQ1.offer(val);

                long newSum1 = cur.sum1 + val;
                long newSum2 = cur.sum2 - val;
                String key = newSum1 + "," + newSum2;

                if (!visited.contains(key)) {
                    visited.add(key);
                    bfsQ.offer(new BfsQElement(cur.count + 1, newQ1, newQ2, newSum1, newSum2));
                }
            }
        }

        return -1;
    }
}
```
