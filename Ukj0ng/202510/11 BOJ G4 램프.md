```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Map<String, Integer> map;
    private static int N, M, K, max;

    public static void main(String[] args) throws IOException {
        init();

        for (String key : map.keySet()) {
            char[] chars = key.toCharArray();
            int count = 0;
            for (char c : chars) {
                if (c == '0') count++;
            }

            if (count <= K && (count%2 == K%2)) max = Math.max(max, map.get(key));
        }

        bw.write(max+"\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        max = 0;

        map = new HashMap<>();

        for (int i = 0; i < N; i++) {
            String input = br.readLine();
            map.put(input, map.getOrDefault(input, 0)+1);
        }
        K = Integer.parseInt(br.readLine());
    }
}
```
