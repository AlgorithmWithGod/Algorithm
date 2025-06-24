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

public class Main {

    static IOController io;

    //

    static int N, Q;
    static TreeSet<Long> S;
    static long[] B;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        S = new TreeSet<>();
        for(int i=0;i<N;i++) S.add(io.nextLong());
        Q = io.nextInt();
        B = new long[Q];
        for(int i=0;i<Q;i++) B[i] = io.nextInt();

    }

    static void solve() throws Exception {

        long sum = 0;
        for(long i:S) sum += i;

        S.add(Long.MAX_VALUE);

        Deque<long[]> list = new ArrayDeque<>();

        long left = N;

        // 처음에 제거되는 경우가 있으면 먼저 처리
        if(S.contains((long)N)) {
            while(left >= 0 && S.contains(left)) S.remove(left--);
            list.offerLast(new long[]{N, left});
        }

        // 추가, 제거 반복
        while(true) {

            long next = S.ceiling(left);
            if(next == Long.MAX_VALUE){
                list.offerLast(new long[]{left, next});
                break;
            }
            S.add(left);
            list.offerLast(new long[]{left, next});
            S.remove(next);
            while(left >= 0 && S.contains(left)) S.remove(left--);
            list.offerLast(new long[]{next, left});

        }

        for(long q : B) {

            while(q > 0) {
                long[] cur = list.pollFirst();
                long l = cur[0], r = cur[1], cnt = Math.abs(l-r);

                if(q < cnt) {
                    if(l > r) {
                        list.offerFirst(new long[]{l-q, r});
                        r = l-q;
                    }
                    else {
                        list.offerFirst(new long[]{l+q, r});
                        r = l+q;
                    }
                    q = 0;
                }
                else q -= cnt;

                if(l > r) {
                    sum -= l*(l+1)/2 - r*(r+1)/2;
                }
                else {
                    sum += (r-1)*r/2 - (l-1)*l/2;
                }

            }

            io.write(sum + "\n");

        }



    }

}
```
