```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int T = Integer.parseInt(br.readLine());

        StringBuilder sb = new StringBuilder();
        while (T-- > 0) {
            String s = br.readLine();
            sb.append(palindrom(s, 0, s.length() - 1, 0)).append("\n");
        }
        System.out.print(sb);
    }

    static int palindrom(String s, int left, int right, int deleted) {
        if (deleted >= 2) return 2;

        while (left < right) {
            if (s.charAt(left) == s.charAt(right)) {
                left++;
                right--;
            } else {
                int resLeft = palindrom(s, left + 1, right, deleted + 1);
                int resRight = palindrom(s, left, right - 1, deleted + 1);

                return Math.min(resLeft, resRight);
            }
        }

        return deleted;
    }
}
```
