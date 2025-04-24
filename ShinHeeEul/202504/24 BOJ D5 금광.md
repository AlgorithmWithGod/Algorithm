```java
import java.util.*;
import java.io.*;

class Main {

    static Node[] segments;
    static long MIN = Long.MIN_VALUE >> 1;
    static Node DEFAULT = new Node(MIN,MIN,MIN,0);
    static int N;
    static int size;
    public static void main(String[] args) throws Exception {

        N = read();

        size = 1;

        while(size < N) size <<= 1;



        // Point 별로 값을 저장해두고, x좌표 순으로 정렬 후 index 매기기
        Point[] arr = new Point[N];

        for(int i = 0; i < N; i++) arr[i] = new Point(read(), read(), 0, read());

        Arrays.sort(arr, (o1, o2) -> {
            if(o1.x == o2.x) return o1.val - o2.val;
            return o1.x - o2.x;
        });

        for(int i = 0; i < N; i++) {
            arr[i].index = i;
            int idx = i;
            while((i + 1) < N && arr[i + 1].x == arr[i].x) {
                arr[i + 1].index = idx;
                i++;
            }
        }
        // 이후 y좌표 순으로 정렬 후
        Arrays.sort(arr, Comparator.comparingInt(p -> p.y));

        // y가 작은 것/큰 것부터 update하면서 해당 인덱스에 업데이트
        long max = Long.MIN_VALUE;



        int nxt = 1;
        for(int k = 0; k < N; k+=nxt) {
            nxt = 1;
            while((k+nxt) < N && arr[k+nxt].y == arr[k].y) {
                nxt++;
            }
            segments = new Node[(size << 1) + 1];
            Arrays.fill(segments, DEFAULT);
            for (int i = k; i < N; i++) {
                Point point = arr[i];
                update(point.index, point.val);

                // y가 같은 값이라면 한번에 업데이트 해야 함.
                while ((i + 1) < N && arr[i + 1].y == point.y) {
                    update(arr[i + 1].index, arr[i + 1].val);
                    i++;
                }
                max = Math.max(max, segments[2].max);
            }
        }

        System.out.println(max);
    }

    public static void update(int idx, int val) {

        idx += size + 1;
        if(segments[idx] == DEFAULT) segments[idx] = new Node(val, val, val, val);
        else {
            segments[idx].lmax += val;
            segments[idx].rmax += val;
            segments[idx].max += val;
            segments[idx].sum += val;
        }
        idx = (idx + 1) >> 1;

        while(idx >= 2) {
            segments[idx] = combine(segments[(idx << 1) - 1], segments[idx << 1]);
            idx = (idx + 1) >> 1;
        }
    }

    public static Node combine(Node lNode, Node rNode) {
        return new Node(
                Math.max(lNode.lmax, lNode.sum + rNode.lmax),
                Math.max(rNode.rmax, rNode.sum + lNode.rmax),
                Math.max(lNode.rmax + rNode.lmax, Math.max(lNode.max, rNode.max)),
                lNode.sum + rNode.sum
        );
    }

    public static class Point {
        int x;
        int y;
        int index;
        int val;

        public Point(int x, int y, int index, int val) {
            this.x = x;
            this.y = y;
            this.index = index;
            this.val = val;
        }
    }

    public static class Node {
        long lmax;
        long rmax;
        long max;
        long sum;

        public Node(long lmax, long rmax, long max, long sum) {
            this.lmax = lmax;
            this.rmax = rmax;
            this.max = max;
            this.sum = sum;
        }

    }

    private static int read() throws Exception {
        int d, o;
        boolean negative = false;
        d = System.in.read();
        if (d == 45) {
            negative = true;
            d = System.in.read();
        }

        o = d & 15;
        while ((d = System.in.read()) > 32)
            o = (o << 3) + (o << 1) + (d & 15);

        return negative ? -o : o;
    }

}
```
