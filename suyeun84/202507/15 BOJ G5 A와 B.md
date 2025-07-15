```java
import java.util.*;
import java.io.*;

public class boj12904 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;

    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}

    static String S;
    public static void main(String[] args) throws Exception {
        nextLine();
        S = st.nextToken();
        nextLine();
        String T = st.nextToken();
        System.out.println(find(T));
    }

    static int find(String curr) {
        int len = curr.length();
        if (S.equals(curr)) return 1;
        else {
            if (len <= 1) return 0;
        }
        if (curr.charAt(len-1) == 'B') {
            StringBuilder sb = new StringBuilder(curr.substring(0, len - 1));
            return find(sb.reverse().toString());
        } else if (curr.charAt(len-1) == 'A') {
            return find(curr.substring(0, len - 1));
        }
        return 0;
    }
}
```
