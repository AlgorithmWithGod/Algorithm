```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int n,m;
    static int[] parent;

    public static void main(String[] args) throws Exception{
        st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        parent = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }

        int ans = 0;
        for (int i = 1; i <= m; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            if(union(a,b)){
                ans = i;
                break;
            }
        }
        bw.write(ans+"");
        bw.close();
    }
    static int find(int cur){
        if(cur == parent[cur]){
            return cur;
        }else{
            return parent[cur] = find(parent[cur]);
        }
    }
    static boolean union(int a, int b){
        int rootA = find(a);
        int rootB = find(b);

        if(rootA == rootB){
            return true;
        }else{
            if(rootA < rootB){
                parent[rootA] = rootB;
            }else{
                parent[rootB] = rootA;
            }
            return false;
        }
    }
}
```
