```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static List<Integer>[] adjList;
    static int[] degree;
    static int[] result;

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        adjList = new List[N+1];
        degree = new int[N+1];
        result = new int[N];

        for (int i = 1; i <= N; i++) {
            adjList[i] = new ArrayList<>();
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int cnt = Integer.parseInt(st.nextToken());
            int[] order = new int[cnt];
            for (int j = 0; j < cnt; j++) {
                order[j] = Integer.parseInt(st.nextToken());
            }
            for (int j = 0; j < cnt-1; j++) {
                for (int k = j+1; k < cnt; k++) {
                    if(!adjList[order[j]].contains(order[k])) {
                        adjList[order[j]].add(order[k]);
                        degree[order[k]]++;
                    }
                }
            }
        }

        if(go() == N){
            for (int i = 0; i < N; i++) {
                bw.write(result[i]+"\n");
            }
        }else{
            bw.write("0");
        }
        bw.close();
    }
    public static int go(){
        int cnt = 0;
        ArrayDeque<Integer> q = new ArrayDeque<>();
        for (int i = 1; i <= N; i++) {
            if(degree[i] == 0){
                q.add(i);
            }
        }

        while(!q.isEmpty()){
            int cur = q.poll();
            result[cnt++] = cur;
            for(int next : adjList[cur]){
                if(--degree[next] == 0){
                    q.add(next);
                }
            }
        }
        return cnt;
    }
}
```
