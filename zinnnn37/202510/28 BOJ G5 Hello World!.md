```java
import java.io.*;

public class BJ_13140_Hello_World {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder sb = new StringBuilder();

    private static int N, hello, world;
    private static int[] nums;
    private static boolean[] isSelected;

    public static void main(String[] args) throws IOException {
        init();
        sol(0);

        bw.write("No Answer");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        nums = new int[7];
        isSelected = new boolean[10];
    }

    private static void sol(int depth) throws IOException {
        if (depth == 7) {
            calc();
            return;
        }

        for (int i = 0; i < 10; i++) {
            if (isSelected[i]) continue;
            if ((depth == 0 || depth == 4) && i == 0) continue;

            nums[depth] = i;
            isSelected[i] = true;
            sol(depth + 1);
            isSelected[i] = false;
        }
    }

    private static void calc() throws IOException {
        int ans = 0;

        hello = nums[0] * 10000 + nums[1] * 1000 + nums[2] * 110 + nums[3];
        world = nums[4] * 10000 + nums[3] * 1000 + nums[5] * 100 + nums[2] * 10 + nums[6];

        ans = hello + world;

        if (ans == N) {
            print();
            System.exit(0);
        }
    }

    private static void print() throws IOException {
        sb.append("  ").append(hello).append("\n");
        sb.append("+ ").append(world).append("\n");
        sb.append("-------\n");
        sb.append(N / 100000 == 0 ? "  " : " ").append(N);
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```