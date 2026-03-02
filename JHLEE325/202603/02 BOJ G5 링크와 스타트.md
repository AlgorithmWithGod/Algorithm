```java
import java.io.*;
import java.util.*;

public class Main {
    
    static int N;
    static int[][] S;
    static boolean[] startTeam;
    static int minDiff = Integer.MAX_VALUE;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        N = Integer.parseInt(br.readLine());
        S = new int[N][N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                S[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        startTeam = new boolean[N];

        divide(0);

        System.out.println(minDiff);
    }

    static void divide(int idx) {
        if (idx == N) {
            calculate();
            return;
        }

        startTeam[idx] = true;
        divide(idx + 1);

        startTeam[idx] = false;
        divide(idx + 1);
    }

    static void calculate() {
        int startSum = 0;
        int linkSum = 0;

        for (int i = 0; i < N; i++) {
            for (int j = i + 1; j < N; j++) {
                if (startTeam[i] && startTeam[j]) {
                    startSum += S[i][j] + S[j][i];
                } else if (!startTeam[i] && !startTeam[j]) {
                    linkSum += S[i][j] + S[j][i];
                }
            }
        }

        int diff = Math.abs(startSum - linkSum);

        if (diff == 0) {
            System.out.println(0);
            System.exit(0);
        }

        minDiff = Math.min(minDiff, diff);
    }
}
```
