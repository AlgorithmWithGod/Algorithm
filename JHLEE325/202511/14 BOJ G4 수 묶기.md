```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        List<Integer> plus = new ArrayList<>();
        List<Integer> minus = new ArrayList<>();
        int ones = 0;
        int zeros = 0;

        for (int i = 0; i < N; i++) {
            int x = Integer.parseInt(br.readLine());
            if (x > 1) plus.add(x);
            else if (x == 1) ones++;
            else if (x == 0) zeros++;
            else minus.add(x);
        }

        int sum = ones;

        Collections.sort(plus, Collections.reverseOrder());
        for (int i = 0; i < plus.size(); i += 2) {
            if (i + 1 < plus.size())
                sum += plus.get(i) * plus.get(i + 1);
            else sum += plus.get(i);
        }

        Collections.sort(minus);
        for (int i = 0; i < minus.size(); i += 2) {
            if (i + 1 < minus.size())
                sum += minus.get(i) * minus.get(i + 1);
            else {
                if (zeros > 0) {
                    zeros--;
                } else {
                    sum += minus.get(i);
                }
            }
        }

        System.out.println(sum);
    }
}
```
