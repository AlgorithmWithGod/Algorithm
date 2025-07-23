```java
import java.awt.*;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;


public class Main {
    static int tc,startNum, from,to;
    static int[][] input;
    static boolean[] primes = new boolean[1000001];
    static int[] dp = new int[1000001];
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        tc = Integer.parseInt(br.readLine());
        input = new int[tc][3];

        for (int i = 0; i < tc; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 3; j++) {
                input[i][j] = Integer.parseInt(st.nextToken());
            }
        }
    }

    private static void process() throws IOException {
        makePrimeList();
        for (int i = 0; i < tc; i++) {
            startNum = input[i][0];
            from  = input[i][1];
            to   = input[i][2];

            Arrays.fill(dp, -1);
            doDp(startNum);
            int count = Integer.MAX_VALUE;

            for (int j = from; j <= to; j++){
                if (dp[j] != -1 && primes[j]){
                    count = Math.min(count, dp[j]);
                }
            }

            sb.append( count==Integer.MAX_VALUE ? -1 : count).append("\n");
        }
    }

    private static void doDp(int startNum) {
        dp[startNum] = 0;
        Queue<Integer> queue = new LinkedList<>();
        queue.add(startNum);

        while (!queue.isEmpty()) {
            int cur = queue.poll();
            int curCount = dp[cur];
            if (cur + 1 <= 1000000 && dp[cur + 1] == -1) {
                dp[cur + 1] = curCount + 1;
                queue.add(cur+1);
            }
            if ( cur -1 > 0 && dp[cur - 1] == -1) {
                dp[cur -1] = curCount + 1;
                queue.add(cur-1);
            }
            if (cur /2 > 0 && dp[cur / 2] == -1) {
                dp[cur /2] = curCount + 1;
                queue.add(cur/2);
            }
            if (cur / 3 > 0 && dp[cur / 3] == -1) {
                dp[cur / 3] = curCount + 1;
                queue.add(cur/3);
            }
        }


    }

    private static void makePrimeList() {
        Arrays.fill(primes, true);
        primes[0] = false;
        primes[1] = false;
        for (int i = 2; i <= 1000000; i++) {
            if (!primes[i]) continue;

            int num = i * 2;
            while (num <= 1000000) {
                primes[num] = false;
                num += i;
            }
        }
    }


    private static void print()  {
        System.out.print(sb.toString());
    }



}


```