```
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] rooms;
    private static int N;
    private static long atk;

    public static void main(String[] args) throws IOException {
        init();
        long answer = binarySearch();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        atk = Long.parseLong(st.nextToken());

        rooms = new int[N+1][3];

        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            rooms[i][0] = Integer.parseInt(st.nextToken());
            rooms[i][1] = Integer.parseInt(st.nextToken());
            rooms[i][2] = Integer.parseInt(st.nextToken());
        }
    }

    private static long binarySearch() {
        long left = 1;
        long right = (long) 9e18;
        long result = 0;

        while (left <= right) {
            long mid = left + (right - left) / 2;

            if (valid(mid, atk)) {
                result = mid;
                right = mid-1;
            } else {
                left = mid+1;
            }
        }

        return result;
    }

    private static boolean valid (long hp, long atk) {
        long maxHp = hp;

        for (int i = 1; i <= N; i++) {
            if (rooms[i][0] == 1) {
                long turn = rooms[i][2] / atk - 1;
                if (rooms[i][2] % atk > 0) turn++;
                turn = Math.max(turn, 0);
                hp -= turn * (long)rooms[i][1];
                if (hp <= 0) {
                    return false;
                }
            } else {
                atk += rooms[i][1];
                hp += rooms[i][2];
                hp = Math.min(hp, maxHp);
            }
        }

        return true;
    }
}
```
