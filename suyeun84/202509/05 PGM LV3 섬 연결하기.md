```java
import java.util.*;
class Solution {
    public int solution(int n, int[][] costs) {
        int answer = 0;
        HashSet<Integer> set = new HashSet<>();
        Arrays.sort(costs, (o1, o2) -> o1[2] - o2[2]);
        set.add(costs[0][0]);
        while (set.size() < n) {
            for (int[] cost : costs) {
                if (set.contains(cost[0]) && set.contains(cost[1])) continue;
                else if (set.contains(cost[0]) || set.contains(cost[1])) {
                    set.add(cost[0]);
                    set.add(cost[1]);
                    answer += cost[2];
                    break;
                }
            }
        }
        return answer;
    }
}
```
