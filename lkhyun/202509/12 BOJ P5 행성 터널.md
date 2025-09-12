```java
import java.io.*;
import java.util.*;

public class Main {
    static class Vertex{
        int num;
        long value;

        public Vertex(int num, long value) {
            this.num = num;
            this.value = value;
        }
    }
    
    static class Edge{
        int from,to;
        long value;

        public Edge(int from, int to, long value) {
            this.from = from;
            this.to = to;
            this.value = value;
        }
    }
    
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static List<long[]> xyz = new ArrayList<>();
    static int[] root;
    static PriorityQueue<Edge> pq = new PriorityQueue<>((a,b) -> Long.compare(a.value, b.value)); 
    
    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        root = new int[N];
        for (int i = 0; i < N; i++) {
            root[i] = i;
        }

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            long x = Long.parseLong(st.nextToken());
            long y = Long.parseLong(st.nextToken());
            long z = Long.parseLong(st.nextToken());
            xyz.add(new long[]{i, x, y, z});
        }

        for (int i = 1; i <= 3; i++) {
            int cur = i;
            Collections.sort(xyz, (a, b) -> Long.compare(a[cur], b[cur]));
            
            for (int j = 0; j < N-1; j++) {
                long[] p1 = xyz.get(j);
                long[] p2 = xyz.get(j+1);
                long cost = Math.abs(p2[cur] - p1[cur]);
                pq.offer(new Edge((int)p1[0], (int)p2[0], cost));
            }
        }

        int cnt = 0;
        long ans = 0;
        while(!pq.isEmpty()) {
            Edge cur = pq.poll();
            if(cnt == N-1) break;
            if(union(cur.from, cur.to)){
                ans += cur.value;
                cnt++;
            }
        }
        bw.write(ans+"");
        bw.close();
    }
    
    public static int find(int cur){
        if(root[cur] == cur) return cur;
        else return root[cur] = find(root[cur]);
    }

    public static boolean union(int a, int b){
        int rootA = find(a);
        int rootB = find(b);
        
        if(rootA == rootB){
            return false;
        }else if(rootA < rootB){
            root[rootA] = rootB;
        }else{
            root[rootB] = rootA;
        }
        return true;
    }
}
```
