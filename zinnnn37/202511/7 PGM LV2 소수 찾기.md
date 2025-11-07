```java
import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

class PGM_LV2_소수_찾기 {

    private static int len;
    private static String num;
    private static boolean[] isPrime, visited;
    private static Set<Integer> set;

    private static void findPrime() {
        Arrays.fill(isPrime, 2, 10000000, true);

        for (int i = 2; i * i <= 10000000; i++) {
            if (isPrime[i]) {
                for (int j = i * i; j < 10000000; j += i) {
                    isPrime[j] = false;
                }
            }
        }
    }

    private static void init(String numbers) {
        num = numbers;
        len = num.length();

        isPrime = new boolean[10000000];
        visited = new boolean[len];

        set = new HashSet<>();

        findPrime();
    }

    private void dfs(int depth, int start, int candidate) {
        if (depth > len) {
            return;
        }

        if (candidate > 0) {
            if (isPrime[candidate]) {
                set.add(candidate);
            }
        }

        for (int i = 0; i < len; i++) {
            if (visited[i]) continue;

            int curNum = num.charAt(i) - '0';

            visited[i] = true;
            dfs(depth + 1, start + 1, candidate * 10 + curNum);
            visited[i] = false;
        }
    }

    public int solution(String numbers) {
        init(numbers);
        dfs(0, 0, 0);
        return set.size();
    }
}
```