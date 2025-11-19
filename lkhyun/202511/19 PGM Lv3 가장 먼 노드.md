```java
import java.util.*;
class Solution {
    static int answer = 0;
    static int max = 0;
    static List<Integer>[] adjList;
    public int solution(int n, int[][] edge) {
        answer = 0;
        adjList = new List[n+1];
        for(int i = 0; i<=n; i++){
            adjList[i] = new ArrayList<>();
        }
        
        for(int[] e : edge){
            int a = e[0];
            int b = e[1];
            adjList[a].add(b);
            adjList[b].add(a);
        }
        
        BFS(n);
        
        return answer;
    }
    public static void BFS(int n){
        ArrayDeque<int[]> q = new ArrayDeque<>();
        boolean[] visited = new boolean[n+1];
        q.offer(new int[]{1,0});
        visited[1] = true;
        
        while(!q.isEmpty()){
            int[] cur = q.poll();
            if(max < cur[1]){
                max = cur[1];
                answer = 1;
            }else if(max == cur[1]){
                answer++;
            }
            for(int next : adjList[cur[0]]){
                if(!visited[next]){
                    q.offer(new int[]{next,cur[1]+1});
                    visited[next] = true;
                }
            }
        }
    }
}
```
