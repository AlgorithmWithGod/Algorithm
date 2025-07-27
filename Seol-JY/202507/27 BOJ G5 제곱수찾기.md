```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class Main {
    static int N, M;
    static int[][] board;
    static int maxSqrt = -1;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String[] sizes = br.readLine().split(" ");
        N = Integer.parseInt(sizes[0]);
        M = Integer.parseInt(sizes[1]);

        board = new int[N][M];
        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < M; j++) {
                board[i][j] = line.charAt(j) - '0';
            }
        }

        for (int row = 0; row < N; row++) {
            for (int col = 0; col < M; col++) {
                for (int dr = -N; dr <= N; dr++) {
                    for (int dc = -M; dc <= M; dc++) {
                        if (dr == 0 && dc == 0) continue;

                        int r = row;
                        int c = col;
                        StringBuilder sb = new StringBuilder();

                        while (r >= 0 && r < N && c >= 0 && c < M) {
                            sb.append(board[r][c]);
                            long num = Long.parseLong(sb.toString());

                            if (isPerfectSquare(num)) {
                                maxSqrt = Math.max(maxSqrt, (int) num);
                                if (maxSqrt >= 31622 * 31622) {
                                    System.out.println(maxSqrt);
                                    return;
                                }
                            }

                            r += dr;
                            c += dc;
                        }
                    }
                }
            }
        }

        System.out.println(maxSqrt);
    }

    static boolean isPerfectSquare(long num) {
        long sqrt = (long) Math.sqrt(num);
        return sqrt * sqrt == num;
    }
}

```
