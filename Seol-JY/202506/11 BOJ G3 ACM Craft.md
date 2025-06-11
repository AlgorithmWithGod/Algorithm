```java
import java.io.*;
import java.util.*;

public class Main {
    private static List<List<Integer>> graph;
    private static int[] indegree, buildTime, minTime;
    private static int N, W;
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        
        int T = Integer.parseInt(br.readLine());
        
        for (int t = 0; t < T; t++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            N = Integer.parseInt(st.nextToken());
            int K = Integer.parseInt(st.nextToken());
            
            buildTime = new int[N + 1];
            st = new StringTokenizer(br.readLine());
            for (int i = 1; i <= N; i++) {
                buildTime[i] = Integer.parseInt(st.nextToken());
            }
            
            graph = new ArrayList<>();
            for (int i = 0; i <= N; i++) {
                graph.add(new ArrayList<>());
            }
            
            indegree = new int[N + 1];
            
            for (int i = 0; i < K; i++) {
                st = new StringTokenizer(br.readLine());
                int X = Integer.parseInt(st.nextToken());
                int Y = Integer.parseInt(st.nextToken());
                
                graph.get(X).add(Y);
                indegree[Y]++;
            }
            
            W = Integer.parseInt(br.readLine());
            
            topologicalSort();
            bw.write(minTime[W] + "\n");
        }
        
        bw.flush();
        bw.close();
        br.close();
    }
    
    private static void topologicalSort() {
        Queue<Integer> queue = new LinkedList<>();
        minTime = new int[N + 1];
        
        for (int i = 1; i <= N; i++) {
            if (indegree[i] == 0) {
                queue.offer(i);
                minTime[i] = buildTime[i];
            }
        }
        
        while (!queue.isEmpty()) {
            int current = queue.poll();
            
            for (int next : graph.get(current)) {
                minTime[next] = Math.max(minTime[next], minTime[current] + buildTime[next]);
                indegree[next]--;
                
                if (indegree[next] == 0) {
                    queue.offer(next);
                }
            }
        }
    }
}
```
