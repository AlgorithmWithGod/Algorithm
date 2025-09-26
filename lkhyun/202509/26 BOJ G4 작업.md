```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static int N;
    static List<Integer>[] prevTask;
    static int[] prevCnt;
    static int[] cost;
    static int ans = 0;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        prevTask = new List[N+1];
        for (int i = 1; i <= N; i++) {
            prevTask[i] = new ArrayList<>();
        }
        prevCnt = new int[N+1];
        cost = new int[N+1];

        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            cost[i] = Integer.parseInt(st.nextToken());
            int tmp = Integer.parseInt(st.nextToken());
            for (int j = 0; j < tmp; j++) {
                prevTask[Integer.parseInt(st.nextToken())].add(i);
                prevCnt[i]++;
            }
        }
        solve();
        bw.write(ans+"");
        bw.close();
    }
    public static void solve(){
        PriorityQueue<int[]> q = new PriorityQueue<>((a,b) -> Integer.compare(a[1],b[1]));
        boolean[] visited = new boolean[N+1];
        for (int i = 1; i <= N; i++) {
            if(prevCnt[i] == 0){
                q.offer(new int[]{i,cost[i]});
                visited[i] = true;
            }
        }

        while(!q.isEmpty()){
            int[] cur = q.poll();
            ans = Math.max(ans,cur[1]);

            for (int next : prevTask[cur[0]]) {
                if(!visited[next]){
                    prevCnt[next]--;
                    if(prevCnt[next] == 0){
                        q.offer(new int[]{next,cur[1]+cost[next]});
                        visited[next] = true;
                    }
                }
            }
        }
    }
}
```
