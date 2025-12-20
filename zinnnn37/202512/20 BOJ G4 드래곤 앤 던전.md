```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_16434_드래곤_앤_던전 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int  N;
    private static long initialPower, ans;
    private static int[][] rooms;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        initialPower = Long.parseLong(st.nextToken());

        rooms = new int[N][3];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            rooms[i][0] = Integer.parseInt(st.nextToken());
            rooms[i][1] = Integer.parseInt(st.nextToken());
            rooms[i][2] = Integer.parseInt(st.nextToken());
        }
    }

    private static void sol() throws IOException {
        long left  = 1;
        long right = (long) 1e18;

        ans = right;
        while (left <= right) {
            long mid = left + (right - left) / 2;

            if (canClear(mid)) {
                ans = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static boolean canClear(long hp) {
        long curHP = hp;
        long power = initialPower;

        for (int i = 0; i < N; i++) {
            int  t = rooms[i][0];
            long a = rooms[i][1];
            long h = rooms[i][2];

            if (t == 1) {
                long attackCnt = (h + power - 1) / power;
                long damage    = a * (attackCnt - 1);

                curHP -= damage;
                if (curHP <= 0) {
                    return false;
                }
            } else {
                power += a;
                curHP = Math.min(hp, curHP + h);
            }
        }
        return true;
    }

}
```