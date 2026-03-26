```java
import java.io.*;
import java.util.*;

public class BOJ13711 {
    static class SegmentTree {
        int[] tree;
        SegmentTree(int size) {
            tree = new int[size*4];
        }

        void update(int s, int e, int i, int v, int n) {
            if(s == e) {
                tree[n] = v;
                return;
            }
            int m = (s+e)>>1;
            if(i <= m)  update(s, m, i, v, n*2);
            else        update(m+1, e, i, v, n*2+1);
            tree[n] = Math.max(tree[n*2], tree[n*2+1]);
        }

        int find(int s, int e, int l, int r, int n) {
            if(l>r || l>e || r<s) return 0;
            if(l<=s && e<=r) return tree[n];
            int m = (s+e)>>1;
            return Math.max(find(s, m, l, r, n*2), find(m+1, e, l, r, n*2+1));
        }
    }

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static int N;
    static int[] index;
    static SegmentTree seg;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());

        index = new int[N+1];
        st = new StringTokenizer(br.readLine());
        for(int i=1;i<=N;i++) {
            index[Integer.parseInt(st.nextToken())] = i;
        }

        seg = new SegmentTree(N);
        st = new StringTokenizer(br.readLine());
        for(int i=1;i<=N;i++) {
            int a = Integer.parseInt(st.nextToken());
            int val = seg.find(1, N, 1, index[a], 1) + 1;
            seg.update(1, N, index[a], val, 1);
        }

        bw.write(seg.tree[1] + "\n");
        bw.close();
    }
}
```
