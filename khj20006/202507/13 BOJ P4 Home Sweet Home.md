```java
import java.util.*;
import java.io.*;

class IOController {
    BufferedReader br;
    BufferedWriter bw;
    StringTokenizer st;

    public IOController() {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer("");
    }

    String nextLine() throws Exception {
        String line = br.readLine();
        st = new StringTokenizer(line);
        return line;
    }

    String nextToken() throws Exception {
        while (!st.hasMoreTokens()) nextLine();
        return st.nextToken();
    }

    int nextInt() throws Exception {
        return Integer.parseInt(nextToken());
    }

    long nextLong() throws Exception {
        return Long.parseLong(nextToken());
    }

    double nextDouble() throws Exception {
        return Double.parseDouble(nextToken());
    }

    void close() throws Exception {
        bw.flush();
        bw.close();
    }

    void write(String content) throws Exception {
        bw.write(content);
    }

}

public class Main {

    static IOController io;

    //

    static final long INF = (long)1e18 + 7;

    static int N, M, K;
    static List<int[]>[] graph;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();
    }

    public static void init() throws Exception {

        N = io.nextInt();
        M = io.nextInt();
        K = io.nextInt();
        graph = new ArrayList[N+1];
        for (int i = 1; i <= N; i++) graph[i] = new ArrayList<>();
        for (int i = 1; i <= M; i++) {
            int a = io.nextInt();
            int b = io.nextInt();
            int c = io.nextInt();
            graph[a].add(new int[]{b,c});
            graph[b].add(new int[]{a,c});
        }

    }

    static void solve() throws Exception {

        // 다익스트라 돌리기
        long[] dist = new long[N+1];
        Arrays.fill(dist, INF);
        PriorityQueue<long[]> pq = new PriorityQueue<>((a,b) -> Long.compare(a[0],b[0]));
        dist[1] = 0;
        pq.offer(new long[]{0,1});
        while(!pq.isEmpty()) {
            long[] cur = pq.poll();
            int n = (int)cur[1];
            long d = cur[0];
            if(d > dist[n]) continue;
            for(int[] e : graph[n]) {
                if(dist[e[0]] > d + e[1]) {
                    dist[e[0]] = d + e[1];
                    pq.offer(new long[]{dist[e[0]], e[0]});
                }
            }
        }

        // dist 정렬
        long[] arr = new long[N];
        for(int i=1;i<=N;i++) arr[i-1] = dist[i];
        Arrays.sort(arr);

        // 단순 그래프를 만족하지 않는 경우 먼저 제외
        long answer = 0;
        for(int i=1;i<=N;i++) for(int[] e:graph[i]) {
            int j = e[0], c = e[1];
            if(i<j) continue;
            answer -= Math.max(0L, (K - Math.abs(dist[i] - dist[j]) + 1));
        }

        // 답 구하기
        long prevSum = 0;
        int lastIndex = 0;
        for(int i=1;i<N;i++) {
            while(arr[i] - arr[lastIndex] > K) {
                prevSum -= arr[lastIndex++];
            }
            answer += (long)(i-lastIndex)*(K-arr[i]+1) + prevSum;
            prevSum += arr[i];
        }

        io.write(answer + "\n");

    }

}
```
