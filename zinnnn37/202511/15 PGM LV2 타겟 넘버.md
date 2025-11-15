```java
public class PGM_LV2_타겟_넘버 {

    private static int target, len, ans;
    private static int[] nums;

    private static void dfs(int start, int sum) {
        if (start == len) {
            if (sum == target) ans++;
            return;
        }

        dfs(start + 1, sum - nums[start]);
        dfs(start + 1, sum + nums[start]);
    }

    public int solution(int[] n, int t) {
        target = t;
        nums = n;
        len = n.length;
        ans = 0;

        dfs(0, 0);

        return ans;
    }

}
```