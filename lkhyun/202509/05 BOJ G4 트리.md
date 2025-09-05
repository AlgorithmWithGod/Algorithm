```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static int N,M;
    static int T;
    public static void main(String[] args) throws Exception {
        T = 1;
        while(true){
            st = new StringTokenizer(br.readLine());
            N = Integer.parseInt(st.nextToken());
            M = Integer.parseInt(st.nextToken());
            if(N == 0 && M == 0) break;
            sb.append("Case ").append(T++).append(": " );

            int[] parent = new int[N+1];
            for (int i = 1; i <= N; i++) {
                parent[i] = i;
            }

            Set<Integer> cycles = new HashSet<>();

            for (int i = 0; i < M; i++) {
                st = new StringTokenizer(br.readLine());
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                union(a, b, parent, cycles);
            }

            Set<Integer> s = new HashSet<>();
            for (int i = 1; i <= N; i++) {
                s.add(find(i,parent));
            }

            for(int c : cycles){
                s.remove(find(c,parent));
            }

            if(s.size()==0){
                sb.append("No trees.\n");
            }else if(s.size()==1){
                sb.append("There is one tree.\n");
            }else{
                sb.append("A forest of ").append(s.size()).append(" trees.\n");
            }
        }
        bw.write(sb.toString());
        bw.close();
    }
    public static int find(int cur, int[] parent){
        if(parent[cur] == cur) return cur;
        else return parent[cur] = find(parent[cur],parent);
    }
    public static void union(int a, int b, int[] parent, Set<Integer> cycles){
        int rootA = find(a,parent);
        int rootB = find(b,parent);
        
        if(rootA < rootB){
            parent[rootA] = rootB;
        }else if(rootA > rootB){
            parent[rootB] = rootA;
        }else{
            cycles.add(rootA);
        }
    }
}
```
