```
import java.io.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static boolean flag;
    private static int[] sum;
    private static char[] input;

    public static void main(String[] args) throws IOException {
        init();
        int answer = solve(flag);

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        input = br.readLine().toCharArray();
        sum = new int[input.length+1];
        int a = 0;
        int b = 0;

        for (int i = 0; i < input.length; i++) {
            if (input[i] == '(') a++;
            else b++;
        }

        // true -> '('가 더 많은 경우
        if (a > b) flag = true;
        // false -> ')'가 더 많은 경우
    }

    private static int solve(boolean flag) {
        int result = 0;

        if (flag) {
            for (int i = 1; i <= input.length; i++) {
                if (input[input.length-i] == ')') sum[i] = sum[i-1]+1;
                else sum[i] = sum[i-1]-1;
                if (sum[i] == -1) {
                    result = (i+1)/2;
                    break;
                }
            }
        } else {
            for (int i = 1; i <= input.length; i++) {
                if (input[i-1] == '(') sum[i] = sum[i-1]+1;
                else sum[i] = sum[i-1]-1;
                if (sum[i] == -1) {
                    result = (i+1)/2;
                    break;
                }
            }
        }

        return result;
    }
}
```
