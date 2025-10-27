```java
import java.io.*;
import java.util.*;

public class Main {
    static int N;
    static int[] next;
    static boolean[] finished;
    static boolean[] inCycle;
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        
        N = Integer.parseInt(br.readLine());
        next = new int[N + 1];
        finished = new boolean[N + 1];
        inCycle = new boolean[N + 1];
        
        for (int i = 1; i <= N; i++) {
            next[i] = Integer.parseInt(br.readLine());
        }
        
        for (int i = 1; i <= N; i++) {
            if (!finished[i]) {
                boolean[] visited = new boolean[N + 1];
                int current = i;
                List<Integer> path = new ArrayList<>();
                
                while (!visited[current] && !finished[current]) {
                    visited[current] = true;
                    path.add(current);
                    current = next[current];
                }
                
                if (!finished[current]) {
                    int cycleStart = current;
                    boolean inCycleNow = false;
                    
                    for (int node : path) {
                        if (node == cycleStart) {
                            inCycleNow = true;
                        }
                        if (inCycleNow) {
                            inCycle[node] = true;
                        }
                        finished[node] = true;
                    }
                } else {
                    for (int node : path) {
                        finished[node] = true;
                    }
                }
            }
        }
        
        List<Integer> result = new ArrayList<>();
        for (int i = 1; i <= N; i++) {
            if (inCycle[i]) {
                result.add(i);
            }
        }
        
        bw.write(result.size() + "\n");
        for (int num : result) {
            bw.write(num + "\n");
        }
        
        bw.flush();
        bw.close();
        br.close();
    }
}
```
