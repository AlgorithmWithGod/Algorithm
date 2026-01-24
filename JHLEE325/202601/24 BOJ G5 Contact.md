```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        while (T-- > 0) {
            String s = br.readLine();
            if (isMatch(s)) System.out.println("YES");
            else System.out.println("NO");
        }
    }

    static boolean isMatch(String s) {
        int state = 0;

        for (char c : s.toCharArray()) {
            int cur = c - '0';

            if (state == 0) {
                state = (cur == 0) ? 1 : 2;
            } else if (state == 1) {
                if (cur == 1) state = 0;
                else return false;
            } else if (state == 2) {
                if (cur == 0) state = 3;
                else return false;
            } else if (state == 3) {
                if (cur == 0) state = 4;
                else return false;
            } else if (state == 4) {
                if (cur == 0) state = 4;
                else state = 5;
            } else if (state == 5) {
                if (cur == 0) state = 6;
                else state = 7;
            } else if (state == 6) {
                if (cur == 0) return false;
                else state = 0;
            } else if (state == 7) {
                if (cur == 0) state = 8;
                else state = 7;
            } else if (state == 8) {
                if (cur == 0) state = 4;
                else state = 0;
            }

            if (state == -1) return false;
        }

        return state == 0 || state == 5 || state == 7;
    }
}
```
