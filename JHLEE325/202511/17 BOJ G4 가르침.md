```java
import java.io.*;
import java.util.*;

public class Main {

    static int N, K;
    static String[] words;
    static boolean[] learned = new boolean[26];
    static int answer = 0;

    static final char[] antic = {'a', 'n', 't', 'i', 'c'};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        words = new String[N];

        for (int i = 0; i < N; i++) {
            words[i] = br.readLine().trim();
        }

        if (K < 5) {
            System.out.println(0);
            return;
        }

        if (K == 26) {
            System.out.println(N);
            return;
        }

        for (char c : antic) {
            learned[c - 'a'] = true;
        }

        dfs(0, 0);

        System.out.println(answer);
    }


    static void dfs(int idx, int count) {
        if (count == K - 5) {
            answer = Math.max(answer, count());
            return;
        }

        if (idx >= 26) return;

        if (learned[idx]) {
            dfs(idx + 1, count);
        } else {
            learned[idx] = true;
            dfs(idx + 1, count + 1);

            learned[idx] = false;
            dfs(idx + 1, count);
        }
    }

    static int count() {
        int cnt = 0;

        for (String word : words) {
            boolean canRead = true;

            for (int i = 0; i < word.length(); i++) {
                char c = word.charAt(i);

                if (!learned[c - 'a']) {
                    canRead = false;
                    break;
                }
            }

            if (canRead) cnt++;
        }

        return cnt;
    }
}
```
