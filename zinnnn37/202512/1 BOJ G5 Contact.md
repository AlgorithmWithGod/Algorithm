```java
import java.io.*;
import java.util.regex.Pattern;

public class BJ_1013_Contact {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder sb = new StringBuilder();

    private static int N;
    private static String input;

    public static void main(String[] args) throws IOException {
        sol();
    }

    private static void sol() throws IOException {
        N = Integer.parseInt(br.readLine());

        while (N-- > 0) {
            input = br.readLine();

            boolean res = Pattern.matches("(100+1+|01)+", input);
            sb.append(res ? "YES\n" : "NO\n");
        }
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```