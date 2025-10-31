```java
import java.io.*;
import java.util.*;

public class Main {
    static int N;
    static ArrayList<Integer> nums = new ArrayList<>();
    static ArrayList<Character> ops = new ArrayList<>();
    static int answer = Integer.MIN_VALUE;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        String str = br.readLine();

        for (int i = 0; i < N; i++) {
            char c = str.charAt(i);
            if (i % 2 == 0) nums.add(c - '0');
            else ops.add(c);
        }

        dfs(0, nums.get(0));
        System.out.println(answer);
    }

    static void dfs(int idx, int sum) {
        if (idx >= ops.size()) {
            answer = Math.max(answer, sum);
            return;
        }

        int cur = calc(sum, ops.get(idx), nums.get(idx + 1));
        dfs(idx + 1, cur);

        if (idx + 1 < ops.size()) {
            int next = calc(nums.get(idx + 1), ops.get(idx + 1), nums.get(idx + 2));
            int cur2 = calc(sum, ops.get(idx), next);
            dfs(idx + 2, cur2);
        }
    }

    static int calc(int a, char op, int b) {
        if (op == '+') return a + b;
        else if (op == '-') return a - b;
        else return a * b;
    }
}
```
