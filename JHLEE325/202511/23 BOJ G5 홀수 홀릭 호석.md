```java
import java.io.*;
import java.util.*;

public class Main {

    static int min = Integer.MAX_VALUE;
    static int max = Integer.MIN_VALUE;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String N = br.readLine();
        dfs(N, 0);

        System.out.println(min + " " + max);
    }

    static void dfs(String num, int totalOdd) {

        int curOdd = countOdd(num);
        totalOdd += curOdd;

        int len = num.length();

        if (len == 1) {
            min = Math.min(min, totalOdd);
            max = Math.max(max, totalOdd);
            return;
        }

        if (len == 2) {
            int sum = (num.charAt(0) - '0') + (num.charAt(1) - '0');
            dfs(String.valueOf(sum), totalOdd);
            return;
        }

        for (int i = 1; i < len - 1; i++) {
            for (int j = i + 1; j < len; j++) {

                int a = Integer.parseInt(num.substring(0, i));
                int b = Integer.parseInt(num.substring(i, j));
                int c = Integer.parseInt(num.substring(j));

                int sum = a + b + c;

                dfs(String.valueOf(sum), totalOdd);
            }
        }
    }

    static int countOdd(String s) {
        int cnt = 0;
        for (char c : s.toCharArray()) {
            if ((c - '0') % 2 == 1) cnt++;
        }
        return cnt;
    }
}
```
