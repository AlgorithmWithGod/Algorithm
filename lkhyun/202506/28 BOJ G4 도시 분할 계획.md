```java
import java.util.*;
import java.io.*;

public class Main{
    static class Edge{
        int u,v,weight;

        Edge(int u,int v,int w){
            this.u=u;
            this.v=v;
            this.weight=w;
        }
    }
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static List<Edge> l;
    static int[] parent;

    public static void main(String[] args) throws Exception{
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        l = new ArrayList<>();
        parent = new int[N+1];
        for (int i = 1; i <= N; i++) {
            parent[i] = i;
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());
            l.add(new Edge(u,v,w));
        }
        l.sort((a, b) -> a.weight - b.weight);

        int count = N-1;
        int sum = 0;
        for(Edge e:l){
            if(merge(e.u,e.v)){
                count--;
                if(count==0){
                    break;
                }
                sum += e.weight;
            }
        }
        bw.write(sum+"\n");
        bw.close();
    }
    static int find(int cur){
        if(parent[cur]==cur){
            return cur;
        }else{
            return parent[cur] = find(parent[cur]);
        }
    }
    static boolean merge(int u, int v){
        int uRoot = find(u);
        int vRoot = find(v);

        if(uRoot==vRoot){
            return false;
        }else{
            if(uRoot<vRoot){
                parent[vRoot] = uRoot;
            }else{
                parent[uRoot] = vRoot;
            }
            return true;
        }
    }
}
```
