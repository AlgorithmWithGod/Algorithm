```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N, K;
    static int[] vehicleTime, vehiclePrice, walkTime, walkPrice;
    static int[] dp;
    static boolean[] impossible;
    
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        walkTime = new int[N + 1];
        walkPrice = new int[N + 1];
        vehicleTime = new int[N + 1];
        vehiclePrice = new int[N + 1];
        dp = new int[K + 1];
        impossible = new boolean[K + 1];

        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            walkTime[i] = Integer.parseInt(st.nextToken());
            walkPrice[i] = Integer.parseInt(st.nextToken());
            vehicleTime[i] = Integer.parseInt(st.nextToken());
            vehiclePrice[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.fill(impossible, true);
        
        if (walkTime[1] <= K) {
            dp[walkTime[1]] = walkPrice[1];
            impossible[walkTime[1]] = false;
        }
        if (vehicleTime[1] <= K) {
            if (impossible[vehicleTime[1]]) {
                dp[vehicleTime[1]] = vehiclePrice[1];
                impossible[vehicleTime[1]] = false;
            } else {
                dp[vehicleTime[1]] = Math.max(dp[vehicleTime[1]], vehiclePrice[1]);
            }
        }

        for (int i = 2; i <= N; i++) {
            boolean[] nextImpossible = new boolean[K + 1];
            Arrays.fill(nextImpossible, true);
            int[] nextDp = new int[K + 1];

            for (int j = K; j >= 0; j--) {
                if (impossible[j]) continue;
                
                if (j + walkTime[i] <= K) {
                    int nextTime = j + walkTime[i];
                    int nextMoney = dp[j] + walkPrice[i];
                    
                    if (nextImpossible[nextTime]) {
                        nextDp[nextTime] = nextMoney;
                        nextImpossible[nextTime] = false;
                    } else {
                        nextDp[nextTime] = Math.max(nextDp[nextTime], nextMoney);
                    }
                }

                if (j + vehicleTime[i] <= K) {
                    int nextTime = j + vehicleTime[i];
                    int nextMoney = dp[j] + vehiclePrice[i];
                    
                    if (nextImpossible[nextTime]) {
                        nextDp[nextTime] = nextMoney;
                        nextImpossible[nextTime] = false;
                    } else {
                        nextDp[nextTime] = Math.max(nextDp[nextTime], nextMoney);
                    }
                }
            }
            
            dp = nextDp;
            impossible = nextImpossible;
        }

        int answer = 0;
        for (int j = 0; j <= K; j++) {
            if (!impossible[j]) {
                answer = Math.max(answer, dp[j]);
            }
        }

        bw.write(answer + "");
        bw.close();
    }
}
```
