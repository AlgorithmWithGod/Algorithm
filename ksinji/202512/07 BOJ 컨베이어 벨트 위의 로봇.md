```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());

        int[] belt = new int[2 * n];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < 2 * n; i++) {
            belt[i] = Integer.parseInt(st.nextToken());
        }

        boolean[] robot = new boolean[n];
        int step = 0;

        while (true) {
            step++;

            // 컨베이어 벨트 회전
            int last = belt[2 * n - 1];
            for (int i = 2 * n - 1; i >= 1; i--) {
                belt[i] = belt[i - 1];
            }
            belt[0] = last;

            for (int i = n - 1; i >= 1; i--) {
                robot[i] = robot[i - 1];
            }
            robot[0] = false;
            robot[n - 1] = false;

            // 로봇 회전
            for (int i = n - 1; i >= 1; i--) {
                if (robot[i - 1] && !robot[i] && belt[i] > 0) {
                    robot[i] = true;
                    robot[i - 1] = false;
                    belt[i]--;
                }
            }
            robot[n - 1] = false;

            // 0번 칸에 로봇 올리기
            if (!robot[0] && belt[0] > 0) {
                robot[0] = true;
                belt[0]--;
            }

            // 내구도가 0인 칸의 개수가 k개 이상이라면 과정을 종료
            int zeroCnt = 0;
            for (int i = 0; i < 2 * n; i++) {
                if (belt[i] == 0) zeroCnt++;
            }
            if (zeroCnt >= k) {
                System.out.println(step);
                break;
            }
        }
    }
}

```
