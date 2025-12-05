```java
import java.io.*;
import java.util.*;

public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        st = new StringTokenizer(br.readLine());
        int[] wok = new int[M];
        for(int i = 0; i < M; i++){
            wok[i] = Integer.parseInt(st.nextToken());
        }

        ArrayList<Integer> cook = new ArrayList<>();
        for(int i = 0; i < M; i++){
            cook.add(wok[i]);
        }
        for(int i = 0; i < M; i++){
            for(int j = i + 1; j < M; j++){
                cook.add(wok[i] + wok[j]);
            }
        }

        int INF = 100_000_000;
        int[] dp = new int[N + 1];
        Arrays.fill(dp, INF);
        dp[0] = 0;
        for(int x = 0; x <= N; x++){
            if(dp[x] == INF)
                continue;
            for(int c : cook){
                int nx = x + c;
                if(nx <= N){
                    dp[nx] = Math.min(dp[nx], dp[x] + 1);
                }
            }
        }
        int answer = dp[N];
        System.out.println((answer >= INF)? -1 : answer);
        
    }
}

```
