```java
import java.io.*;
import java.util.*;

public class Main {

    static ArrayList<Long> list = new ArrayList<>();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());

        for (int i = 0; i <= 9; i++) {
            dfs(i, 1);
        }

        Collections.sort(list);

        if (n >= list.size()) {
            System.out.println(-1);
        } else {
            System.out.println(list.get(n));
        }
    }

    static void dfs(long num, int depth) {
        list.add(num);

        long lastDigit = num % 10;
        if (lastDigit == 0) return;
        
        for (int next = 0; next < lastDigit; next++) {
            dfs(num * 10 + next, depth + 1);
        }
    }
}
```
