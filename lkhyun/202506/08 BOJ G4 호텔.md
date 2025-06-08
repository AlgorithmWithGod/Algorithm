```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int C,N;
    static int[] cost;
    static int[] client;
    static int[] dp;

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine());
        C = Integer.parseInt(st.nextToken());
        N = Integer.parseInt(st.nextToken());

        cost = new int[N];
        client = new int[N];
        dp = new int[1200]; //인덱스만큼의 인원을 홍보할때 그 비용
        Arrays.fill(dp,Integer.MAX_VALUE);
        dp[0] = 0;

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            cost[i] = Integer.parseInt(st.nextToken()); //홍보 비용
            client[i] = Integer.parseInt(st.nextToken()); //홍보했을때 얻는 고객 수
        }

        for (int i = 0; i < N; i++) {//모든 도시에 대해
            for (int j = client[i]; j < dp.length; j++) {
                if(dp[j-client[i]] != Integer.MAX_VALUE) {
                    dp[j] = Math.min(dp[j], dp[j-client[i]] + cost[i]);
                }
            }
        }
        int min = Integer.MAX_VALUE;
        for (int i = C; i < dp.length ; i++) {
            min = Math.min(min, dp[i]);
        }
        bw.write(min + "");
        bw.close();
    }
}
```