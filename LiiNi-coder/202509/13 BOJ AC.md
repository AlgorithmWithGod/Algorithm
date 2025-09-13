```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.StringTokenizer;

public class Main {
    private static BufferedReader br;
    private static StringBuilder sb;

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        sb = new StringBuilder();

        int T = Integer.parseInt(br.readLine());

        for (int t = 0; t < T; t++) {
            String p = br.readLine();
            int n = Integer.parseInt(br.readLine());
            String arrStr = br.readLine();

            Deque<Integer> q = new ArrayDeque<>();
            if (n > 0) {
                arrStr = arrStr.substring(1, arrStr.length() - 1);
                StringTokenizer st = new StringTokenizer(arrStr, ",");
                for (int i = 0; i < n; i++) {
                    q.addLast(Integer.parseInt(st.nextToken()));
                }
            }

            boolean reversed = false;
            boolean error = false;
            for (char c : p.toCharArray()) {
                if (c == 'R') {
                    reversed = !reversed;
                } else if (c == 'D') {
                    if (q.isEmpty()) {
                        sb.append("error\n");
                        error = true;
                        break;
                    }
                    if (!reversed) q.pollFirst();
                    else q.pollLast();
                }
            }

            if (!error) {
                sb.append("[");
                if (!q.isEmpty()) {
                    if (!reversed) {
                        while (!q.isEmpty()) {
                            sb.append(q.pollFirst());
                            if (!q.isEmpty()) sb.append(",");
                        }
                    } else {
                        while (!q.isEmpty()) {
                            sb.append(q.pollLast());
                            if (!q.isEmpty()) sb.append(",");
                        }
                    }
                }
                sb.append("]\n");
            }
        }

        System.out.print(sb.toString());
    }
}

```
