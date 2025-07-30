```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;
import java.util.TreeMap;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        for(int t = 0; t<T; t++){
            int K = Integer.parseInt(br.readLine());
            TreeMap<Integer, Integer> map = new TreeMap<>();

            for (int i = 0; i < K; i++) {
                StringTokenizer st = new StringTokenizer(br.readLine());
                String command = st.nextToken();
                int value = Integer.parseInt(st.nextToken());

                if (command.equals("I")) {
                    map.put(value, map.getOrDefault(value, 0) + 1);
                } else if (command.equals("D")) {
                    if (map.isEmpty())
                        continue;
                    int key = (value == 1) ? map.lastKey() : map.firstKey();
                    int count = map.get(key);
                    if (count == 1) {
                        map.remove(key);
                    } else {
                        map.put(key, count - 1);
                    }
                }
            }
            if (map.isEmpty()) {
                System.out.println("EMPTY");
            } else {
                System.out.println(map.lastKey() + " " + map.firstKey());
            }
        }
    }
}
```
