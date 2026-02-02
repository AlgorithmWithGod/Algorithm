```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());

        ArrayList<Integer> list = new ArrayList<>();

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            list.add(Integer.parseInt(st.nextToken()));
        }

        int s = Integer.parseInt(br.readLine());

        for (int i = 0; i < n && s > 0; i++) {
            int maxVal = -1;
            int maxIdx = -1;

            int limit = Math.min(i + s, n - 1);

            for (int j = i; j <= limit; j++) {
                if (list.get(j) > maxVal) {
                    maxVal = list.get(j);
                    maxIdx = j;
                }
            }

            list.remove(maxIdx);
            list.add(i, maxVal);

            s -= (maxIdx - i);
        }

        StringBuilder sb = new StringBuilder();
        for (int num : list) {
            sb.append(num).append(" ");
        }
        System.out.println(sb.toString());
    }
}
```
