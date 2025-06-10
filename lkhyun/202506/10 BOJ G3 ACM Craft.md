```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,K;
    static int[] duration;
    static List<Integer>[] adjList;
    static int[] degree;
    static int[] minTime;
    static int goal;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());
        for (int t = 1; t <= T; t++) {
            st = new StringTokenizer(br.readLine());
            N = Integer.parseInt(st.nextToken());
            K = Integer.parseInt(st.nextToken());
            duration = new int[N+1];
            adjList = new List[N+1];
            degree = new int[N+1];
            minTime = new int[N+1];

            st = new StringTokenizer(br.readLine());
            for (int i = 1; i <= N; i++) {
                duration[i] = Integer.parseInt(st.nextToken());
                minTime[i] = duration[i];
            }
            for (int i = 1; i <= N; i++) {
                adjList[i] = new ArrayList<>();
            }
            for (int i = 0; i < K; i++) {
                st = new StringTokenizer(br.readLine());
                int first = Integer.parseInt(st.nextToken());
                int second = Integer.parseInt(st.nextToken());
                adjList[first].add(second);
                degree[second]++;
            }
            goal = Integer.parseInt(br.readLine());

            go();
        }

        bw.close();
    }
    public static void go() throws IOException {
        ArrayDeque<Integer> q = new ArrayDeque<>();
        for (int i = 1; i <= N; i++) {
            if(degree[i] == 0){
                q.add(i);
            }
        }

        while(!q.isEmpty()) {
            int cur = q.poll();
            for (int next : adjList[cur]) {
                minTime[next] = Math.max(minTime[next], minTime[cur]+duration[next]);

                degree[next]--;
                if(degree[next] == 0){
                    q.add(next);
                }
            }
        }
        bw.write(minTime[goal]+"\n");
    }
}
```
