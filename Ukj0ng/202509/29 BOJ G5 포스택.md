```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Stack<Integer>[] stacks;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();

        int answer = 0;
        for (int i = 0; i < 4; i++) {
            answer += stacks[i].size();
        }

        if (answer-4 == N) bw.write("YES");
        else bw.write("NO");

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        stacks = new Stack[4];

        for (int i = 0; i < 4; i++) {
            stacks[i] = new Stack<>();
            stacks[i].push(0);
        }

        N = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());

        for (int i = 0; i < N; i++) {
            int num = Integer.parseInt(st.nextToken());
            int min = N;
            int index = -1;

            for (int j = 0; j < 4; j++) {
                if (stacks[j].peek() == 0) {
                    index = j;
                    continue;
                }
                int temp = num - stacks[j].peek();
                if (temp < 0) continue;
                if (temp < min) {
                    index = j;
                    min = temp;
                }
            }

            if (index > -1) stacks[index].push(num);
        }
    }
}
```
