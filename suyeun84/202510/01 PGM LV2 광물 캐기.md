```java
import java.util.*;

class Solution {
    public int solution(int[] picks, String[] minerals) {
        int answer = 0;

        int totalPicks = picks[0] + picks[1] + picks[2];
        int limit = Math.min(minerals.length, totalPicks * 5);

        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> {
            if (b[0] != a[0]) return b[0] - a[0];
            if (b[1] != a[1]) return b[1] - a[1];
            return b[2] - a[2]; 
        });

        int dia = 0, iron = 0, stone = 0, cnt = 0;

        for (int i = 0; i < limit; i++) {
            String m = minerals[i];
            if (m.equals("diamond")) {
                dia += 1; iron += 5; stone += 25;
            } else if (m.equals("iron")) {
                dia += 1; iron += 1; stone += 5;
            } else {
                dia += 1; iron += 1; stone += 1;
            }
            cnt++;

            if (cnt == 5) {
                pq.offer(new int[]{stone, iron, dia});
                dia = iron = stone = 0;
                cnt = 0;
            }
        }
        if (cnt > 0) {
            pq.offer(new int[]{stone, iron, dia});
        }

        while (!pq.isEmpty() && (picks[0] + picks[1] + picks[2] > 0)) {
            int[] g = pq.poll();
            if (picks[0] > 0) {
                answer += g[2];
                picks[0]--;
            } else if (picks[1] > 0) { 
                answer += g[1];
                picks[1]--;
            } else {                 answer += g[0];
                picks[2]--;
            }
        }

        return answer;
    }
}

```
