```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int K;
    static int V, E;
    static List<Integer>[] adjLists;

    public static void main(String[] args) throws IOException {
        K = Integer.parseInt(br.readLine());
        
        for (int i = 0; i < K; i++) {
            st = new StringTokenizer(br.readLine());
            V = Integer.parseInt(st.nextToken());
            E = Integer.parseInt(st.nextToken());
            adjLists = new List[V + 1];
            for (int j = 1; j <= V; j++) {
                adjLists[j] = new ArrayList<>();
            }
            for (int j = 0; j < E; j++) {
                st = new StringTokenizer(br.readLine());
                int u = Integer.parseInt(st.nextToken());
                int v = Integer.parseInt(st.nextToken());
                adjLists[u].add(v);
                adjLists[v].add(u);
            }
            if (!BFS()) {
                bw.write("NO\n");
            } else {
                bw.write("YES\n");
            }
        }
        bw.close();
    }

    public static boolean BFS() {
        ArrayDeque<Integer> q = new ArrayDeque<>();
        int[] visited = new int[V+1];
        
        for (int i = 1; i <= V; i++) {
            if (visited[i] == 0) {  
                q.offer(i);
                visited[i] = 1;  
                
                while (!q.isEmpty()) {
                    int cur = q.poll();
                    
                    for (int next : adjLists[cur]) {
                        if (visited[next] == 0) {
                            visited[next] = -visited[cur];
                            q.offer(next);
                        } else if (visited[next] == visited[cur]) {
                            
                            return false;
                        }
                    }
                }
            }
        }
        return true;
    }
}

```
