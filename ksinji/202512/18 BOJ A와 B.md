```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String s = br.readLine();
        String t = br.readLine();
       
        char[] a = t.toCharArray();
        int l = 0;
        int r = a.length - 1;
        boolean dir = false;

        while (r - l + 1 > s.length()) {
            char last = dir ? a[l] : a[r];
            if (last == 'A') {
                if (dir) l++;
                else r--;
            } else {
                if (dir) l++;
                else r--;
                dir = !dir;
            }
        }

        for (int i = 0; i < s.length(); i++) {
            char c = dir ? a[r - i] : a[l + i];
            if (c != s.charAt(i)) {
                System.out.print(0);
                return;
            }
        }

        System.out.print(1);
    }
}
```