```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) throws IOException {
        var br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        char[] src = br.readLine().toCharArray();
        char[] dst = br.readLine().toCharArray();
        int answer = process(Arrays.copyOf(src, n), dst, false);
        answer = Math.min(answer, process(Arrays.copyOf(src, n), dst, true));
        
        System.out.println(answer == Integer.MAX_VALUE ? -1 : answer);
    }
    static int process(char[] s, char[] target, boolean firstPress) {
        int count = 0;
        // 첫번째 토글로 그리디 분기
        if (firstPress) {
            toggle(s, 0);
            toggle(s, 1);
            count++;
        }
        for (int i = 1; i < s.length; i++) {
            if (s[i - 1] != target[i - 1]) {
                toggle(s, i - 1);
                toggle(s, i);
                if (i + 1 < s.length)
                    toggle(s, i + 1);
                count++;
            }
        }

        for (int i = 0; i < s.length; i++) {
            if (s[i] != target[i]) return Integer.MAX_VALUE;
        }
        return count;
    }

    static void toggle(char[] arr, int i) {
        arr[i] = arr[i] == '0' ? '1' : '0';
    }
}
```
