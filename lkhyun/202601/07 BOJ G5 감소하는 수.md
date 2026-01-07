```java

import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        List<Long> list = new ArrayList<>();

        for (int i = 1; i < 1024; i++) {
            long num = 0;
            for (int j = 9; j >= 0; j--) {
                if ((i & (1 << j)) != 0) {
                    num = num * 10 + j;
                }
            }
            list.add(num);
        }

        Collections.sort(list);

        System.out.println(N >= list.size() ? -1 : list.get(N));
    }
}
```
