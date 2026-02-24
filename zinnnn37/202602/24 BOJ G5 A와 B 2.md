```java
import java.io.*;

public class BJ_12919_A와_B_2 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    private static int    res;
    private static String from, to;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        from = br.readLine();
        to = br.readLine();
    }

    private static void sol() throws IOException {
        bw.write(rec(to) + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static int rec(String to) throws IOException {
        if (from.equals(to)) {
            return 1;
        }

        if (to.length() < from.length()) {
            return 0;
        }

        if (to.charAt(to.length() - 1) == 'A') {
            res = rec(to.substring(0, to.length() - 1));
        }

        if (to.charAt(0) == 'B') {
            StringBuilder tmp = new StringBuilder(to.substring(1));
            res = Math.max(res, rec(tmp.reverse().toString()));
        }
        return res;
    }

}
```