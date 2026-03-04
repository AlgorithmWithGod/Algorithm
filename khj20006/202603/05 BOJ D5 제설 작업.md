```java
import java.io.*;
import java.util.*;

public class BOJ34757 {

    static class IOManager {
        static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        static StringTokenizer st = new StringTokenizer("");

        private IOManager(){}

        static String nextLine() throws Exception {
            return br.readLine();
        }

        static String nextToken() throws Exception {
            while (!st.hasMoreTokens()) {
                st = new StringTokenizer(nextLine());
            }
            return st.nextToken();
        }

        static int nextInt() throws Exception {
            return Integer.parseInt(nextToken());
        }

        static long nextLong() throws Exception {
            return Long.parseLong(nextToken());
        }

        static double nextDouble() throws Exception {
            return Double.parseDouble(nextToken());
        }

        static void write(String content) throws Exception {
            bw.write(content);
        }

        public static void close() throws Exception {
            bw.flush();
            bw.close();
            br.close();
        }
    }

    //

    static class Node {
        int left, right;
        long amount;
        Node(int left, int right, long amount) {
            this.left = left;
            this.right = right;
            this.amount = amount;
        }
    }

    static class Query extends Node implements Comparable<Query> {
        int lo, hi, mid, num;
        Query(int left, int right, long amount, int lo, int hi, int num) {
            super(left, right, amount);
            this.lo = lo;
            this.hi = hi;
            this.mid = (lo + hi) / 2;
            this.num = num;
        }

        @Override
        public int compareTo(Query o) {
            if ((this.lo + this.hi) / 2 == (o.lo + o.hi) / 2) {
                return this.num - o.num;
            }
            return (this.lo + this.hi) / 2 - (o.lo + o.hi) / 2;
        }
    }

    static class DisjointSet {
        int[] root;

        DisjointSet() {}

        void init(int size) {
            root = new int[size + 2];
            for(int i=1;i<=size + 1;i++) {
                root[i] = i;
            }
        }

        int find(int x) {
            return x == root[x] ? x : (root[x] = find(root[x]));
        }

        void union(int a, int b) {
            int x = find(a), y = find(b);
            if(x == y) {
                return;
            }
            root[x] = y;
        }
    }

    static class SegmentTree {
        long[] tree;

        SegmentTree() {}

        void init(int size) {
            tree = new long[size * 4];
        }

        void update(int s, int e, int i, long v, int n) {
            if(s == e) {
                tree[n] += v;
                return;
            }
            int m = (s+e)>>1;
            if(i <= m) {
                update(s, m, i, v, n*2);
            }
            else {
                update(m+1, e, i, v, n*2+1);
            }
            tree[n] = tree[n*2] + tree[n*2+1];
        }

        long rangeSum(int s, int e, int l, int r, int n) {
            if(l > r || l > e || r < s) {
                return 0;
            }
            if(l <= s && e <= r) {
                return tree[n];
            }
            int m = (s+e)>>1;
            return rangeSum(s, m, l, r, n*2) + rangeSum(m+1, e, l, r, n*2+1);
        }
    }

    static int N, M, Q;
    static long[] snow;
    static Node[] works;
    static PriorityQueue<Query> queries;
    static SegmentTree seg = new SegmentTree();
    static DisjointSet ds = new DisjointSet();
    static int[] answer;

    public static void main(String[] args) throws Exception {
        N = IOManager.nextInt();
        M = IOManager.nextInt();
        Q = IOManager.nextInt();

        snow = new long[N+2];
        for(int i=1;i<=N;i++) {
            snow[i] = IOManager.nextLong();
        }

        works = new Node[M];
        for(int i=0;i<M;i++) {
            int left = IOManager.nextInt();
            int right = IOManager.nextInt();
            long amount = IOManager.nextLong();
            works[i] = new Node(left, right, amount);
        }

        queries = new PriorityQueue<>();
        for(int i=0;i<Q;i++) {
            int left = IOManager.nextInt();
            int right = IOManager.nextInt();
            long amount = IOManager.nextLong();
            queries.add(new Query(left, right, amount, 0, M, i));
        }

        answer = new int[Q];
        while(!queries.isEmpty()) {
            seg.init(N);
            ds.init(N);
            PriorityQueue<Query> temp = new PriorityQueue<>();
            for(int i=0;i<M;i++) {
                int left = works[i].left, right = works[i].right;
                long amount = works[i].amount;

                int x = ds.find(left);
                while(amount > 0 && x <= right) {
                    long cur = seg.rangeSum(1, N, x, x, 1);
                    long diff = Math.min(snow[x] - cur, amount);
                    amount -= diff;
                    seg.update(1, N, x, diff, 1);
                    if (cur + diff == snow[x]) {
                        ds.union(x, x + 1);
                        x = ds.find(x + 1);
                    }
                }

                while(!queries.isEmpty() && queries.peek().mid == i) {
                    Query query = queries.poll();
                    long sum = seg.rangeSum(1, N, query.left, query.right, 1);
                    if (sum >= query.amount) {
                        query.hi = query.mid;
                    }
                    else {
                        query.lo = query.mid + 1;
                    }
                    query.mid = (query.lo + query.hi) / 2;

                    if(query.lo >= query.hi) {
                        answer[query.num] = query.lo + 1;
                        if(query.lo == M) {
                            answer[query.num] = -1;
                        }
                    }
                    else {
                        if(query.mid != M) {
                            temp.add(query);
                        }
                    }
                }
            }
            queries = temp;
        }

        for(int i=0;i<Q;i++) {
            IOManager.write(answer[i] + "\n");
        }

        IOManager.close();
    }

}

```
