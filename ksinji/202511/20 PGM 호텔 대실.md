```java
import java.util.*;

class Solution {
    public int solution(String[][] book_time) {
        int n = book_time.length;
        int[][] times = new int[n][2];
        
        for (int i = 0; i < n; i++) {
            int start = toMinutes(book_time[i][0]);
            int end = toMinutes(book_time[i][1]) + 10;
            
            times[i][0] = start;
            times[i][1] = end;
        }

        Arrays.sort(times, (a, b) -> a[0] - b[0]);

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        int answer = 0;
        for (int i = 0; i < n; i++) {
            int start = times[i][0];
            int end = times[i][1];

            while (!pq.isEmpty() && pq.peek() <= start) {
                pq.poll();
            }

            pq.offer(end);

            answer = Math.max(answer, pq.size());
        }

        return answer;
    }

    private int toMinutes(String time) {
        String[] temp = time.split(":");
        int h = Integer.parseInt(temp[0]);
        int m = Integer.parseInt(temp[1]);
        return h * 60 + m;
    }
}

```
