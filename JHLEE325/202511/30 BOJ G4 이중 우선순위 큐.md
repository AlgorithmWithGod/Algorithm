```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int T = Integer.parseInt(br.readLine());

        for (int t = 0; t < T; t++) {
            int K = Integer.parseInt(br.readLine());
            TreeMap<Integer, Integer> map = new TreeMap<>();

            for (int i = 0; i < K; i++) {
                st = new StringTokenizer(br.readLine());
                char op = st.nextToken().charAt(0);
                int num = Integer.parseInt(st.nextToken());

                if (op == 'I') {
                    map.put(num, map.getOrDefault(num, 0) + 1);
                }
                else {
                    if (map.isEmpty()) {
                        continue;
                    }

                    int key;

                    if (num == 1) {
                        key = map.lastKey();
                    }
                    else {
                        key = map.firstKey();
                    }

                    int cnt = map.get(key);
                    if (cnt == 1) {
                        map.remove(key);
                    } else {
                        map.put(key, cnt - 1);
                    }
                }
            }

            if (map.isEmpty()) {
                System.out.println("EMPTY");
            } else {
                int max = map.lastKey();
                int min = map.firstKey();
                System.out.println(max + " " + min);
            }
        }
    }
}
```
