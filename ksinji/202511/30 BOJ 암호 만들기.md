```java
import java.io.*;
import java.util.*;

public class Main {
    static int l, c;
    static char[] chars;
    static char[] selected;
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        l = Integer.parseInt(st.nextToken());
        c = Integer.parseInt(st.nextToken());

        chars = new char[c];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < c; i++) {
            chars[i] = st.nextToken().charAt(0);
        }

        Arrays.sort(chars);

        selected = new char[l];

        dfs(0, 0, 0, 0);

        System.out.print(sb);
    }

    static void dfs(int idx, int depth, int vowel, int consonant) {
        if (depth == l) {
            if (vowel >= 1 && consonant >= 2) {
                sb.append(selected).append('\n');
            }
            return;
        }

        if (idx == c) {
            return;
        }

        char ch = chars[idx];
        selected[depth] = ch;
        if (isVowel(ch)) {
            dfs(idx + 1, depth + 1, vowel+ 1, consonant);
        } else {
            dfs(idx + 1, depth + 1, vowel, consonant + 1);
        }

        dfs(idx + 1, depth, vowel, consonant);
    }

    static boolean isVowel(char c) {
        return c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u';
    }
}
```
