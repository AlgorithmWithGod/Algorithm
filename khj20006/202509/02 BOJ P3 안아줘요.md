```java
import java.util.*;
import java.io.*;

class IOController {
    BufferedReader br;
    BufferedWriter bw;
    StringTokenizer st;

    public IOController() {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer("");
    }

    String nextLine() throws Exception {
        String line = br.readLine();
        st = new StringTokenizer(line);
        return line;
    }

    String nextToken() throws Exception {
        while (!st.hasMoreTokens()) nextLine();
        return st.nextToken();
    }

    int nextInt() throws Exception {
        return Integer.parseInt(nextToken());
    }

    long nextLong() throws Exception {
        return Long.parseLong(nextToken());
    }

    double nextDouble() throws Exception {
        return Double.parseDouble(nextToken());
    }

    void close() throws Exception {
        bw.flush();
        bw.close();
    }

    void write(String content) throws Exception {
        bw.write(content);
    }

}

class SegTree {
    int[] tree;
    SegTree(int size) {
        tree = new int[size*4];
    }

    void update(int s, int e, int i, int v, int n) {
        if(s == e) {
            tree[n] = Math.max(tree[n], v);
            return;
        }
        int m = (s+e)>>1;
        if(i <= m) update(s,m,i,v,n*2);
        else update(m+1,e,i,v,n*2+1);
        tree[n] = Math.max(tree[n*2],tree[n*2+1]);
    }

    int find(int s, int e, int l, int r, int n) {
        if(l>r || l>e || r<s) return 0;
        if(l<=s && e<=r) return tree[n];
        int m = (s+e)>>1;
        return Math.max(find(s,m,l,r,n*2), find(m+1,e,l,r,n*2+1));
    }
}

public class Main {

    static IOController io;

    //

    static int N, Q;
    static int[][] points;
    static SegTree seg1, seg2;

    static int index(List<Integer> arr, int x) {
        int s = 0, e = arr.size(), m = (s+e)>>1;
        while(s<e) {
            int v = arr.get(m);
            if(v < x) s = m+1;
            else e = m;
            m = (s+e)>>1;
        }
        return m;
    }

    public static void main(String[] args) throws Exception {

        io = new IOController();

        N = io.nextInt();
        Q = io.nextInt();
        points = new int[N][];
        List<Integer> list1 = new ArrayList<>();
        List<Integer> list2 = new ArrayList<>();
        for(int i=0;i<N;i++) {
            points[i] = new int[]{io.nextInt(),io.nextInt(),i+1};
            list1.add(points[i][1]-points[i][0]);
            list2.add(points[i][1]+points[i][0]);
        }

        Collections.sort(list1);
        Collections.sort(list2);

        List<Integer> arr1 = new ArrayList<>();
        List<Integer> arr2 = new ArrayList<>();
        arr1.add(list1.get(0));
        for(int i=1;i<N;i++) if(!list1.get(i).equals(list1.get(i-1))) arr1.add(list1.get(i));
        arr2.add(list2.get(0));
        for(int i=1;i<N;i++) if(!list2.get(i).equals(list2.get(i-1))) arr2.add(list2.get(i));

        seg1 = new SegTree(arr1.size());
        seg2 = new SegTree(arr2.size());

        int[] ans = new int[N+1];
        Arrays.sort(points, (a,b) -> a[1]==b[1] ? a[0]-b[0] : a[1]-b[1]);
        for(int i=0;i<N;) {
            int Y = points[i][1];
            List<int[]> update1 = new ArrayList<>();
            List<int[]> update2 = new ArrayList<>();
            while(i<N && points[i][1] == Y) {
                int x = points[i][0], y = points[i][1], n = points[i][2];
                int i1 = index(arr1, y-x), i2 = index(arr2, y+x);
                ans[n] = Math.max(seg1.find(0,arr1.size()-1,i1,arr1.size()-1,1), seg2.find(0,arr2.size()-1,i2,arr2.size()-1,1)) + 1;
                update1.add(new int[]{i1,ans[n]});
                update2.add(new int[]{i2,ans[n]});
                i++;
            }
            for(int[] up : update1) seg1.update(0,arr1.size()-1,up[0],up[1],1);
            for(int[] up : update2) seg2.update(0,arr2.size()-1,up[0],up[1],1);
        }

        while(Q-->0) io.write(ans[io.nextInt()] + "\n");

        io.close();

    }

}
```
