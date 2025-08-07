```java
import java.io.*;
import java.util.*;

public class Main {

    static int n, k, l;
    static int[][] board;
    static Deque<int[]> snake = new ArrayDeque<>();
    static Map<Integer, Character> dirMap = new HashMap<>();

    static int[][] dir = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        n = Integer.parseInt(br.readLine());
        k = Integer.parseInt(br.readLine());
        board = new int[n][n];

        for (int i = 0; i < k; i++) {
            st = new StringTokenizer(br.readLine());
            int r = Integer.parseInt(st.nextToken()) - 1;
            int c = Integer.parseInt(st.nextToken()) - 1;
            board[r][c] = 2;
        }

        l = Integer.parseInt(br.readLine());
        for (int i = 0; i < l; i++) {
            st = new StringTokenizer(br.readLine());
            int t = Integer.parseInt(st.nextToken());
            char d = st.nextToken().charAt(0);
            dirMap.put(t, d);
        }

        System.out.println(simulate());
    }

    static int simulate() {
        int time = 0;
        int direction = 0;
        int x = 0, y = 0;

        snake.offerLast(new int[]{y, x});
        board[y][x] = 1;

        while (true) {
            time++;
            int dy = y + dir[direction][0];
            int dx = x + dir[direction][1];

            if (!(0 <= dy && dy < n && 0 <= dx && dx < n) || board[dy][dx] == 1) break;

            if (board[dy][dx] == 2) {
                board[dy][dx] = 1;
                snake.offerLast(new int[]{dy, dx});
            } else {
                board[dy][dx] = 1;
                snake.offerLast(new int[]{dy, dx});
                int[] tail = snake.pollFirst();
                board[tail[0]][tail[1]] = 0;
            }

            if (dirMap.containsKey(time)) {
                char turn = dirMap.get(time);
                if (turn == 'L') direction = (direction + 3) % 4;
                else if (turn == 'D') direction = (direction + 1) % 4;
            }

            y = dy;
            x = dx;
        }

        return time;
    }

}

```
