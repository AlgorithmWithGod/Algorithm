```java
import java.util.*;
class Solution {
    static List<Integer>[] adjList;
    public int solution(int n, int[][] wires) {
        int answer = n;
        adjList = new List[n+1];
        for(int i = 0; i<=n; i++){
            adjList[i] = new ArrayList<>();
        }
        for(int[] wire : wires){
            adjList[wire[0]].add(wire[1]);
            adjList[wire[1]].add(wire[0]);
        }
        for(int[] wire : wires){
            answer = Math.min(answer,Math.abs(n-(2*BFS(n, wire[0],wire[1]))));    
        }
        
        return answer;
    }
    public int BFS(int n, int start, int except){
        int count = 0;
        ArrayDeque<Integer> q = new ArrayDeque<>();
        boolean[] visited = new boolean[n+1];
        q.offer(start);
        visited[start] = true;
        count++;
        
        while(!q.isEmpty()){
            int cur = q.poll();
            
            for(int next : adjList[cur]){
                if(visited[next] || next == except) continue;
                q.offer(next);
                visited[next] = true;
                count++;
            }
        }
        return count;
    }
}
```
