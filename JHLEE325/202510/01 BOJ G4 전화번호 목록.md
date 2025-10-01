```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();

        int T = Integer.parseInt(br.readLine());

        for (int t = 0; t < T; t++) {
            int n = Integer.parseInt(br.readLine());

            String[] phone = new String[n];

            for (int i = 0; i < n; i++) {
                phone[i] = br.readLine();
            }

            Arrays.sort(phone);

            boolean available = true;
            for (int i = 0; i < n - 1; i++) {
                if (phone[i + 1].startsWith(phone[i])) {
                    available = false;
                    break;
                }
            }

            sb.append(available ? "YES\n" : "NO\n");
        }

        System.out.print(sb.toString());
    }

}
```
