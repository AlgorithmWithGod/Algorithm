```
import java.io.*;
import java.util.*;

public class Main {
    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Map<Character, Integer> map;
    private static char[] input;
    private static int N;
    public static void main(String[] args) throws IOException {
        init();

        int answer = twoPointer();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        map = new HashMap<>();
        input = br.readLine().toCharArray();
    }

    private static int twoPointer() {
        int left = 0;
        int right = 0;
        int max = 0;
        int count = 0;

        while (left < input.length) {
            if (right < input.length && valid(input[right])) {
                map.put(input[right], map.getOrDefault(input[right], 0)+1);
                count++;
                max = Math.max(max, count);
                right++;
            } else {
                map.put(input[left], map.get(input[left])-1);
                if (map.get(input[left]) == 0) {
                    map.remove(input[left]);
                }
                left++;
                count--;
            }
        }

        return max;
    }

    private static boolean valid(char c) {
        return (map.containsKey(c) && map.size() <= N) || (!map.containsKey(c) && map.size() < N);
    }

}
```
