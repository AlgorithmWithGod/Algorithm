```java
import java.io.*;
import java.util.*;

public class Main {
    static int L, C;
    static char[] chars;
    static StringBuilder sb = new StringBuilder();
    static Set<Character> vowels = Set.of('a', 'e', 'i', 'o', 'u');

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        L = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());
        
        chars = new char[C];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < C; i++) {
            chars[i] = st.nextToken().charAt(0);
        }
        
        Arrays.sort(chars); // 정렬해두면 자연스럽게 사전순으로 탐색
        
        backtrack(0, new char[L], 0);
        
        System.out.print(sb);
    }

    static void backtrack(int start, char[] password, int depth) {
        if (depth == L) {
            if (isValid(password)) {
                sb.append(password).append('\n');
            }
            return;
        }
        
        for (int i = start; i < C; i++) {
            password[depth] = chars[i];
            backtrack(i + 1, password, depth + 1);
        }
    }

    static boolean isValid(char[] password) {
        int vowelCount = 0;
        int consonantCount = 0;
        
        for (char c : password) {
            if (vowels.contains(c)) {
                vowelCount++;
            } else {
                consonantCount++;
            }
        }
        
        return vowelCount >= 1 && consonantCount >= 2;
    }
}
```
