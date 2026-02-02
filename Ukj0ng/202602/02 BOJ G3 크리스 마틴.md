```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Map<Character, Integer> map;
    private static char answer;
    private static int N, count;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(count + "\n");
        for (int i = 0; i < N; i++) {
            bw.write(answer + "");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        count = N;
        char[] input = br.readLine().toCharArray();

        map = new HashMap<>();

        map.put('A', 0);
        map.put('C', 0);
        map.put('G', 0);
        map.put('T', 0);
        for (int i = 0; i < N; i++) {
            map.put(input[i], map.get(input[i])+1);
        }

        for (char key : map.keySet()) {
            if (count > map.get(key)) {
                count = map.get(key);
                answer = key;
            }
        }
    }
}
```
