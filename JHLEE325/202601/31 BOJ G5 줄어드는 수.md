```java
import java.util.*;
import java.io.*;

public class Main {

    static int[] nums = {9, 8, 7, 6, 5, 4, 3, 2, 1, 0};
    static List<Long> list = new ArrayList<>();

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        for (int i = 0; i <= 9; i++) {
            dfs(i, i);
        }

        Collections.sort(list);

        if (N > list.size()) {
            System.out.println("-1");
        } else {
            System.out.println(list.get(N - 1));
        }
    }

    static void dfs(long num, int lastDigit) {
        list.add(num);

        for (int i = 0; i < lastDigit; i++) {
            dfs(num * 10 + i, i);
        }
    }
    
}
```
