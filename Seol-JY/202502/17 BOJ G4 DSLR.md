```java
import java.io.*;
import java.util.*;

public class Main {
    static class State {
        int num;
        String commands;
        
        State(int num, String commands) {
            this.num = num;
            this.commands = commands;
        }
    }
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        for (int i = 0; i < T; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());

            String result = bfs(from, to);
            System.out.println(result);
        }
    }

    private static String bfs(int from, int to) {
        Queue<State> queue = new LinkedList<>();
        boolean[] visited = new boolean[10000];
        
        queue.offer(new State(from, ""));
        visited[from] = true;
        
        while (!queue.isEmpty()) {
            State current = queue.poll();
            
            if (current.num == to) {
                return current.commands;
            }
            
            int D = (current.num * 2) % 10000;
            if (!visited[D]) {
                visited[D] = true;
                queue.offer(new State(D, current.commands + "D"));
            }
            
            int S = current.num == 0 ? 9999 : current.num - 1;
            if (!visited[S]) {
                visited[S] = true;
                queue.offer(new State(S, current.commands + "S"));
            }
            
            int L = (current.num % 1000) * 10 + current.num / 1000;
            if (!visited[L]) {
                visited[L] = true;
                queue.offer(new State(L, current.commands + "L"));
            }
            
            int R = (current.num % 10) * 1000 + current.num / 10;
            if (!visited[R]) {
                visited[R] = true;
                queue.offer(new State(R, current.commands + "R"));
            }
        }
        
        return "";
    }
}
```
