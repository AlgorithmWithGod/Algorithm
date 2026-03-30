```java
import java.io.*;
import java.util.*;

public class BOJ2843 {
    static class DisjointSet {
        int[] root;
        DisjointSet(int size) {
            root = new int[size+1];
            for(int i=0;i<=size;i++) {
                root[i] = i;
            }
        }

        int find(int x) {
            return x == root[x] ? x : (root[x] = find(root[x]));
        }

        boolean union(int a, int b) {
            int x = find(a), y = find(b);
            if(x == y) return false;
            root[x] = y;
            return true;
        }
    }
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static int N, Q;
    static int[] arr;
    static int[][] queries;
    static boolean[] check;
    static DisjointSet ds;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());

        arr = new int[N+1];
        check = new boolean[N+1];
        st = new StringTokenizer(br.readLine());
        for(int i=1;i<=N;i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        Q = Integer.parseInt(br.readLine());
        queries = new int[Q][];
        for(int i=0;i<Q;i++) {
            st = new StringTokenizer(br.readLine());
            int op = Integer.parseInt(st.nextToken());
            int x = Integer.parseInt(st.nextToken());
            if(op == 2) {
                check[x] = true;
            }
            queries[i] = new int[]{op, x};
        }

        ds = new DisjointSet(N);

        for(int i=1;i<=N;i++) if(!check[i] && arr[i] != 0) {
            if(!ds.union(i, arr[i])) {
                ds.union(i, 0);
            }
        }

        Stack<String> answer = new Stack<>();
        for(int i=Q-1;i>=0;i--) {
            int op = queries[i][0], x = queries[i][1];
            if(op == 2) {
                if(arr[x] != 0 && !ds.union(x, arr[x])) {
                    ds.union(x, 0);
                }
            }
            else {
                int r = ds.find(x);
                if(r == 0) {
                    answer.add("CIKLUS");
                }
                else {
                    answer.add(Integer.toString(r));
                }
            }
        }

        while(!answer.isEmpty()) {
            bw.write(answer.pop() + "\n");
        }
        
        bw.close();
    }
}
```
