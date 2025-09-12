	```java
import java.util.*;
class Solution {
    static int answer = 0;
    public int solution(int n, int[][] q, int[] ans) {
        List<Integer> list = new LinkedList<>();
        dfs(n, 1, list, q, ans);
        
        return answer;
    }
    
    private void dfs(int n, int idx, List<Integer> list, int[][] q, int[] ans) {
        if (list.size() == 5) {
            if(check(list, q, ans)) {
                answer++;
            }
            return;
        }
        for (int i = idx; i <= n; i++) {
            list.add(i);
            dfs(n, i+1, list, q, ans);
            list.remove(list.size() - 1);
        }
    }
    
    private boolean check(List<Integer> list, int[][] q, int[] ans) {
        int idx = 0;
        for (int[] n : q) {
            int cnt = 0;
            for (int val : n) {
                if (list.contains(val)) cnt++;
            }
            if (cnt != ans[idx]) return false;
            idx++;
        }
        return true;
    }
}
```
