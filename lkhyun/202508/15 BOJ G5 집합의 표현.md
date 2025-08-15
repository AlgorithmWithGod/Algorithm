```java
import java.io.*;
import java.util.*;

public class Main {
    static int N,M;
    static int[] root;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        root = new int[N+1];

        for (int i = 0; i <= N; i++) {
            root[i] = i;
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());

            int cmd = Integer.parseInt(st.nextToken());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            if(cmd == 0){ //합
                union(a,b);
            }else if(cmd == 1){ //같이 있나?
                if(find(a) == find(b)){
                    bw.write("yes\n");
                }else{
                    bw.write("no\n");
                }
            }
        }

        bw.close();
    }

    static int find(int cur){
        if(cur == root[cur]) return cur;
        else{
            return root[cur] = find(root[cur]);
        }
    }
    static void union(int a, int b){
        int rootA = find(a);
        int rootB = find(b);

        if(rootA < rootB){
            root[rootB] = rootA;
        }else{
            root[rootA] = rootB;
        }
    }
}
```
