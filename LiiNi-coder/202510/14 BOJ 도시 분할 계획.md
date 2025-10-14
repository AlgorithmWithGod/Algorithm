```java
import java.io.*;
import java.util.*;

public class Main {
    private static int N, M;
    private static int[] Parent;
    private static List<Edge> Edges = new ArrayList<>();

    private static class Edge implements Comparable<Edge> {
        int from, to, cost;
        Edge(int from, int to, int cost) {
            this.from = from;
            this.to = to;
            this.cost = cost;
        }
        @Override
        public int compareTo(Edge e) {
            return this.cost - e.cost;
        }
    }

    public static void main(String[] args)throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        Parent = new int[N+1];


        for(int i=1; i<=N; i++){
            Parent[i] = i;
        }

        for(int i=0; i<M; i++){
            st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            Edges.add(new Edge(from, to,cost));
        }

        Collections.sort(Edges);
        int answer = 0;
        int countOfEdge = 0;

        for(Edge e : Edges){
            if(countOfEdge == N-2)
                break;
            if(union(e.from,e.to)){
                answer += e.cost;
                countOfEdge++;
            }
        }

        System.out.println(answer);
        br.close();
    }

    private static boolean union(int a, int b){
        a = find(a);
        b = find(b);
        if(a==b)
            return false;
        Parent[b] = a;
        return true;
    }

    private static int find(int x){
        if(Parent[x]==x){
            return x;

        }
        Parent[x] = find(Parent[x]);
        return Parent[x];
    }

}

```
