```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());
        
        int minMoves = bfs(n);
        
        if (minMoves <= k) {
            System.out.println("minigimbob");
        } else {
            System.out.println("water");
        }
    }
    
    static int bfs(int n) {
        if (n == 0) return 0;
        
        Queue<int[]> queue = new LinkedList<>();
        boolean[] visited = new boolean[n + 1];
        
        queue.offer(new int[]{0, 0});
        visited[0] = true;
        
        while (!queue.isEmpty()) {
            int[] cur = queue.poll();
            int pos = cur[0];
            int moves = cur[1];
            
            int next1 = pos + 1;
            if (next1 == n) return moves + 1;
            if (next1 < n && !visited[next1]) {
                visited[next1] = true;
                queue.offer(new int[]{next1, moves + 1});
            }
            
            int next2 = pos + pos / 2;
            if (next2 == n) return moves + 1;
            if (next2 < n && !visited[next2]) {
                visited[next2] = true;
                queue.offer(new int[]{next2, moves + 1});
            }
        }
        
        return Integer.MAX_VALUE;
    }
}
```
