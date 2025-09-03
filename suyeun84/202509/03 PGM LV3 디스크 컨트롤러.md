	'''java
import java.util.*;
class Solution {
    public int solution(int[][] jobs) {
        int answer = 0;
        jobs.add(new int[]{1, 1});
        Arrays.sort(jobs, (o1, o2) -> Integer.compare(o1[0], o2[0]));
        PriorityQueue<int[]> pq = new PriorityQueue<>((o1, o2) -> Integer.compare(o1[0], o2[0]));
        int curr_time = 0;
        int curr_idx = 0;
        int cnt = 0;
        while (cnt < jobs.length) {
            while (curr_idx < jobs.length && jobs[curr_idx][0] <= curr_time) {
                pq.add(new int[]{jobs[curr_idx][1], jobs[curr_idx][0]}); //(걸리는 시간, 시작 시간)
                curr_idx += 1;
            }
            if (!pq.isEmpty()) {
                int[] time = pq.poll();
                cnt += 1;
                answer += (curr_time - time[1] + time[0]);
                curr_time += time[0];
            } else {
                curr_time += 1;
            }
        }
        return answer / jobs.length;
    }
}
```
