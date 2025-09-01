```java
import java.util.*;
class Solution {
    int[] answer;
    int[] result;
    List<Integer> graph[];
    
    public int[] solution(int n, int[][] roads, int[] sources, int destination) {
        answer = new int[n+1];
        result = new int[sources.length];
        graph = new ArrayList[n+1];
        Arrays.fill(answer, -1);
        
        for (int i = 0; i < n+1; i++) {
            graph[i] = new ArrayList<>();
        }
        
        for (int[] road : roads) {
            graph[road[0]].add(road[1]);
            graph[road[1]].add(road[0]);
        }
        
        bfs(destination);
        
        for (int i = 0; i < sources.length; i++) {
            result[i] = answer[sources[i]];
        }
        return result;
    }
    public void bfs(int start) {
        Queue<Integer> q = new ArrayDeque<>();
        q.add(start);
        answer[start] = 0;
        while (!q.isEmpty()) {
            int curr = q.poll();
            for (int next : graph[curr]) {
                if (answer[next] == -1) {
                    answer[next] = answer[curr] + 1;
                    q.add(next);
                }
            }
        }
    }
}
```
