```java
class Main {


    static int size;
    static int N;
    static long[] segments;
    public static void main(String[] args) throws Exception {

        N = read();

        size = 1;

        while(size < N) size <<= 1;

        segments = new long[(size << 1) + 1];

        for(int i = size + 1; i < size + N + 1; i++) segments[i] = read();

        int segmentSize = segments.length - 1;

        while(segmentSize >= 2) {
            segments[segmentSize >> 1] = segments[segmentSize] + segments[segmentSize - 1];
            segmentSize -= 2;
        }

        int Q = read();
        StringBuilder sb = new StringBuilder();

        while(Q --> 0) {
            char c = (char) System.in.read();
            System.in.read();
            int a = read();
            int b = read();

            if(c == 'R') sb.append(query(a, b, 2, 1, size)).append("\n");
            else update(a, b);
        }
        System.out.println(sb);
    }

    public static void update(int idx, int val) {

        idx += size;

        while(idx >= 2) {
            segments[idx] += val;
            idx = (idx + 1) >> 1;
        }
    }

    public static long query(int left, int right, int node, int start, int end) {

        if(end < left || right < start) return 0L;

        if(left <= start && end <= right) return segments[node];

        int mid = (start + end) >> 1;

        return query(left, right, (node << 1) - 1, start, mid)
                + query(left, right, (node << 1), mid + 1, end);
    }

    private static int read() throws Exception {
        int d, o;
        d = System.in.read();

        o = d & 15;
        while (true) {
            d = System.in.read();
            if (d == -1 || Character.isWhitespace(d)) break;
            o = (o << 3) + (o << 1) + (d & 15);
        }

        return o;
    }


}
```
