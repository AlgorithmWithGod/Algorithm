```java
import java.io.*;
import java.util.*;

public class Main {
    static boolean[] isPrime = new boolean[10000];

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        Arrays.fill(isPrime, true);
        isPrime[0] = isPrime[1] = false;
        for (int i = 2; i * i < 10000; i++) {
            if (isPrime[i]) {
                for (int j = i * i; j < 10000; j += i) isPrime[j] = false;
            }
        }

        int T = Integer.parseInt(br.readLine());
        for (int t = 0; t < T; t++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());

            int result = bfs(start, end);
            System.out.println(result == -1 ? "Impossible" : result);
        }
    }

    static int bfs(int start, int end) {
        Queue<Integer> q = new LinkedList<>();
        int[] dist = new int[10000];
        Arrays.fill(dist, -1);

        q.add(start);
        dist[start] = 0;

        while (!q.isEmpty()) {
            int curr = q.poll();
            if (curr == end) return dist[curr];

            for (int i = 0; i < 4; i++) {
                int[] digits = getDigits(curr);

                for (int d = 0; d <= 9; d++) {
                    if (i == 3 && d == 0) continue;

                    int next = changeDigit(digits, i, d);

                    if (isPrime[next] && dist[next] == -1) {
                        dist[next] = dist[curr] + 1;
                        q.add(next);
                    }
                }
            }
        }
        return -1;
    }

    static int[] getDigits(int num) {
        int[] digits = new int[4];
        for (int i = 0; i < 4; i++) {
            digits[i] = num % 10;
            num /= 10;
        }
        return digits;
    }

    static int changeDigit(int[] digits, int idx, int d) {
        int res = 0;
        int p = 1;
        for (int i = 0; i < 4; i++) {
            if (i == idx) res += d * p;
            else res += digits[i] * p;
            p *= 10;
        }
        return res;
    }
}
```
