```java
import java.io.*;
import java.util.*;

public class Main {

    static final double EPS = 1e-6;
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int size = Integer.parseInt(br.readLine());

        for (int t = 0; t < size; t++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            double[] nums = new double[4];
            for (int i = 0; i < 4; i++) nums[i] = Double.parseDouble(st.nextToken());

            boolean ok = canMake24(nums);
            sb.append(ok ? "YES" : "NO").append('\n');
        }
        System.out.print(sb.toString());
    }

    private static boolean canMake24(double[] arr) {
        List<Double> list = new ArrayList<>(4);
        for (double v : arr) list.add(v);
        return dfs(list);
    }

    private static boolean dfs(List<Double> nums) {
        int n = nums.size();
        if (n == 1) {
            return Math.abs(nums.get(0) - 24.0) < EPS;
        }

        // 두 수 선택해서 하나로 줄이기
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                double a = nums.get(i), b = nums.get(j);
                List<Double> nextCandidates = new ArrayList<>(6);

                // 덧셈/곱셈은 교환법칙이 있어 한 번만 추가
                nextCandidates.add(a + b);
                nextCandidates.add(a * b);

                // 뺄셈/나눗셈은 순서가 중요하므로 양쪽 모두 시도
                nextCandidates.add(a - b);
                nextCandidates.add(b - a);
                if (Math.abs(b) > EPS) nextCandidates.add(a / b);
                if (Math.abs(a) > EPS) nextCandidates.add(b / a);

                // 선택한 두 수를 제외한 나머지에 후보 결과를 붙여서 재귀
                for (double cand : nextCandidates) {
                    List<Double> next = new ArrayList<>(n - 1);
                    for (int k = 0; k < n; k++) {
                        if (k == i || k == j) continue;
                        next.add(nums.get(k));
                    }
                    next.add(cand);

                    if (dfs(next)) return true; // 해 찾으면 바로 종료
                }
            }
        }
        return false;
    }
}

```