```java
import java.io.*;
import java.util.*;

public class boj2624 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int T = nextInt();
		nextLine();
		int k = nextInt();
		Coin[] coins = new Coin[k+1];
		int[][] dp = new int[T+1][k+1];
		
		for (int i = 1; i <= k; i++) {
			nextLine();
			int p = nextInt();
			int n = nextInt();
			coins[i] = new Coin(p, n);
		}
		for (int i = 1; i <= k; i++) {
            int val = coins[i].val;
            int cnt = coins[i].cnt;
            dp[0][i - 1] = 1;

            for (int j = 1; j <= cnt; j++) {
                for (int z = val * j; z <= T; z++) {
                    dp[z][i] += dp[z - (val * j)][i - 1];
                }
            }

            for (int j = 1; j <= T; j++) {
                dp[j][i] += dp[j][i - 1];
            }
        }

        System.out.println(dp[T][k]);
	}
	static class Coin {
        int val, cnt;
        Coin(int val, int cnt) {
            this.val = val;
            this.cnt = cnt;
        }
    }
}
```
