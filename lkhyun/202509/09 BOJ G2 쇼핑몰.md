```java

import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static int N,K;
    static PriorityQueue<long[]> in;
    static PriorityQueue<long[]> out;
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        in = new PriorityQueue<>((a,b) -> {
            if(a[0] == b[0]){ //시간이 같으면
                return Long.compare(a[1], b[1]); //적은 번호에 해당하는 곳
            }else{
                return Long.compare(a[0], b[0]);
            }
        });
        out = new PriorityQueue<>((a,b) -> {
            if(a[0] == b[0]){ //시간이 같으면
                return Long.compare(b[1], a[1]); //큰 번호에 해당하는 곳
            }else{
                return Long.compare(a[0], b[0]);
            }
        });
        for (int i = 1; i <= K; i++) {
            in.offer(new long[]{0,i});
        }
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int num = Integer.parseInt(st.nextToken());
            int time = Integer.parseInt(st.nextToken());
            long[] insert = in.poll();
            insert[0] += time;
            in.offer(insert);
            out.offer(new long[]{insert[0],insert[1],num});
        }

        long ans = 0;
        for (int i = 1; i <= N; i++) {
            ans += i*out.poll()[2];
        }
        bw.write(ans+"");
        bw.close();
    }

}
```
