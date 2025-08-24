```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    

    public static void main(String[] args) throws IOException {
        int testcase = Integer.parseInt(br.readLine());
        for(int t = 1 ; t <= testcase ; t++){
            bw.write("Scenario " + t + ":\n");
            int n = Integer.parseInt(br.readLine());
            int k = Integer.parseInt(br.readLine());
            int[] root = new int[n+1];
            for (int i = 0; i < n; i++) {
                root[i] = i;
            }

            for (int i = 0; i < k; i++) {
                st = new StringTokenizer(br.readLine());
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                union(a,b,root);
            }

            int m = Integer.parseInt(br.readLine());
            for (int i = 0; i < m; i++) {
                st = new StringTokenizer(br.readLine());
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                if(find(a,root) == find(b,root)) bw.write("1\n");
                else bw.write("0\n");
            }
            bw.write("\n");
        }

        bw.close();
    }
    public static int find(int cur, int[] root){
        if(cur == root[cur]) return cur;
        else return root[cur] = find(root[cur], root); 
    }
    public static void union(int a,int b, int[] root){
        int rootA = find(a, root);
        int rootB = find(b, root);

        if(rootA != rootB){
            if(rootA < rootB){
                root[rootA] = rootB;
            }else{
                root[rootB] = rootA;
            }
        }
    }
}

```
