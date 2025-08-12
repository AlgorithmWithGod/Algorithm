```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;
import java.util.ArrayList;
import java.util.Collections;

public class Main {
    private static BufferedReader br;
    private static StringTokenizer st;
    private static int N;
    private static int[] arr;
    private static boolean[] visited;
    private static boolean[] onPath;
    private static ArrayList<Integer> result;

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine().trim());
        arr = new int[N + 1];
        for (int i = 1; i <= N; i++) {
            arr[i] = Integer.parseInt(br.readLine().trim());
        }
        visited = new boolean[N + 1];
        result = new ArrayList<>();
        for (int i = 1; i <= N; i++) {
            onPath = new boolean[N + 1];
            dfs(i, i);
        }

        Collections.sort(result);
        System.out.println(result.size());
        for (int num : result) {
            System.out.println(num);
        }

    }

    private static void dfs(int start, int current) {
        if (onPath[current]) {
            if (current == start) {
                result.add(start);
            }
            return;
        }
        onPath[current] = true;
        int next = arr[current];
        dfs(start, next);
        onPath[current] = false;
    }
}
```
