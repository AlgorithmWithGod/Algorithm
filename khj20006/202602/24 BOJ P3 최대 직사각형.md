```java
import java.io.*;
import java.util.*;

public class Main {

    static class IOManager {
        static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        static StringTokenizer st = new StringTokenizer("");

        private IOManager(){}

        static String nextLine() throws Exception {
            String line = br.readLine();
            st = new StringTokenizer(line);
            return line;
        }

        static String nextToken() throws Exception {
            while (!st.hasMoreTokens())
                nextLine();
            return st.nextToken();
        }

        static int nextInt() throws Exception {
            return Integer.parseInt(nextToken());
        }

        static long nextLong() throws Exception {
            return Long.parseLong(nextToken());
        }

        static double nextDouble() throws Exception {
            return Double.parseDouble(nextToken());
        }

        static void write(String content) throws Exception {
            bw.write(content);
        }

        public static void close() throws Exception {
            bw.flush();
            bw.close();
            br.close();
        }
    }

    //

    static int N, M;
    static int[] arr;

    public static void main(String[] args) throws Exception {
        N = IOManager.nextInt();
        M = IOManager.nextInt();
        while (Math.min(N, M) > 0) {
            int ans = 0;
            arr = new int[M];
            for (int i = 0; i < N; i++) {
                for (int j = 0, a; j < M; j++) {
                    a = IOManager.nextInt();
                    if (a == 1) {
                        arr[j]++;
                    }
                    else {
                        arr[j] = 0;
                    }
                }
                ans = Math.max(ans, histogram(arr));
            }

            IOManager.write(ans + "\n");
            N = IOManager.nextInt();
            M = IOManager.nextInt();
        }
        IOManager.close();
    }

    public static int histogram(int[] hist) {
        int ret = 0;
        Stack<int[]> stack = new Stack<>();
        for (int i = 0; i < hist.length; i++) {
            int idx = i;
            while (!stack.isEmpty() && stack.peek()[0] > hist[i]) {
                ret = Math.max(ret, stack.peek()[0] * (i - stack.peek()[1]));
                idx = stack.peek()[1];
                stack.pop();
            }
            stack.push(new int[]{ hist[i], idx });
        }
        while (!stack.isEmpty()) {
            ret = Math.max(ret, stack.peek()[0] * (hist.length - stack.peek()[1]));
            stack.pop();
        }
        return ret;
    }

}
```
