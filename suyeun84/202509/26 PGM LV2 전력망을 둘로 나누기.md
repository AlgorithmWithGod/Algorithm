```java
import java.util.*;
class Solution {
    static int N;
    static List<List<Integer>> graph;
    public int solution(int n, int[][] wires) {
        int answer = Integer.MAX_VALUE;
        N = n;
        graph = new ArrayList<>();
        for (int i = 0; i <= n; i++) graph.add(new ArrayList<>());
        for (int i = 0; i < n-1; i++) {
            graph.get(wires[i][0]).add(wires[i][1]);
            graph.get(wires[i][1]).add(wires[i][0]);
        }
        for (int i = 0; i < n-1; i++) {
            answer = Math.min(answer, check(wires[i][0], wires[i][1]));
        }
        
        return answer;
    }
    
    private int check(int a, int b) {
        Queue<Integer> q = new LinkedList<>();
        boolean[] visited = new boolean[N+1];
        int cnt = 1;
        visited[1] = true;
        q.add(1);
        while(!q.isEmpty()) {
            int curr = q.poll();
            for (int next : graph.get(curr)) {
                if (visited[next] || (a==curr && b==next) || (a==next && b==curr)) continue;
                cnt++;
                visited[next] = true;
                q.add(next);
            }
        }
        return Math.abs((N-cnt) - cnt);
    }
}
```
