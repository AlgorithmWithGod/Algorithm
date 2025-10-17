```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Main {
    static int n;
    static int[][][][] dp;
    static int[] start, goal;
    static final int INF = 1000000000;
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        
        String startStr = br.readLine();
        String goalStr = br.readLine();
        
        start = new int[105];
        goal = new int[105];
        dp = new int[105][10][10][10];
        
        // dp 배열 -1로 초기화
        for (int i = 0; i < 105; i++) {
            for (int j = 0; j < 10; j++) {
                for (int k = 0; k < 10; k++) {
                    Arrays.fill(dp[i][j][k], -1);
                }
            }
        }
        
        // 입력 처리
        for (int i = 0; i < n; i++) {
            start[i] = startStr.charAt(i) - '0';
            goal[i] = goalStr.charAt(i) - '0';
        }
        
        System.out.println(memo(0, start[0], start[1], start[2]));
    }
    
    static int memo(int curr, int a, int b, int c) {
        if (curr == n) {
            return 0;
        }
        
        if (dp[curr][a][b][c] != -1) {
            return dp[curr][a][b][c];
        }
        
        int ret = INF;
        
        // 시계방향(+1)과 반시계방향(-1)
        for (int i = -1; i <= 1; i += 2) {
            // 현재 위치를 목표값으로 맞추는데 필요한 이동량
            int mov = rot(rot(goal[curr] - a) * i);
            
            // j: curr+1이 함께 회전하는 양
            for (int j = 0; j <= mov; j++) {
                // k: curr+2가 함께 회전하는 양
                for (int k = 0; k <= j; k++) {
                    int nb = rot(b + j * i);
                    int nc = rot(c + k * i);
                    
                    // 각각 따로 회전하는 횟수 계산
                    int cost = turn(mov - j) + turn(j - k) + turn(k);
                    int tmp = cost + memo(curr + 1, nb, nc, start[curr + 3]);
                    
                    ret = Math.min(ret, tmp);
                }
            }
        }
        
        return dp[curr][a][b][c] = ret;
    }
    
    // 음수 처리를 위한 회전 함수
    static int rot(int x) {
        while (x < 0) {
            x += 10;
        }
        return x % 10;
    }
    
    // 회전 횟수 계산 (올림 처리)
    static int turn(int x) {
        return x / 3 + (x % 3 != 0 ? 1 : 0);
    }
}
```
