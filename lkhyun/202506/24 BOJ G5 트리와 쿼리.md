```java
import java.util.*;
import java.io.*;
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,R,Q;
    static List<Integer>[] adjList;
    static int[] count;
    static boolean[] visited;


    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());
        Q = Integer.parseInt(st.nextToken());

        adjList = new List[N+1];
        for (int i = 1; i <= N; i++) {
            adjList[i] = new ArrayList<>();
        }

        for (int i = 1; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            adjList[u].add(v);
            adjList[v].add(u);
        }
        count = new int[N+1];
        visited = new boolean[N+1];
        find(R);

        for (int i = 0; i < Q; i++) {
            int start = Integer.parseInt(br.readLine());
            bw.write(count[start] + "\n");
        }
        bw.close();
    }
    static int find(int u) {
        if(visited[u]) return 0;
        int cnt = 1;
        visited[u] = true;

        for(int v : adjList[u]) {
            cnt += find(v);
        }
        count[u] = cnt;
        return cnt;
    }
}

```
