```java
import java.util.*;

class Solution {
    private static boolean[] visited;
    private static HashSet<Integer> set;
    private static char[] nums;

    public int solution(String numbers) {
        nums = numbers.toCharArray();
        visited = new boolean[nums.length];
        set = new HashSet<>();
        
        
        dfs("", 0);
        int answer = 0;
        for(int n : set){
            if(isPrime(n)){
                answer++;
            }
        }
        return answer;
    }

    private void dfs(String now, int depth){
        if(now.length() > 0){
            set.add(Integer.parseInt(now));
        }
        if(depth == nums.length){
            return;
        }

        for(int i = 0; i < nums.length; i++){
            if(visited[i]){
                continue;
            }
            visited[i] = true;
            dfs(now + nums[i], depth + 1); // String + char 가능
            visited[i] = false;
        }
    }

    private boolean isPrime(int n){
        if(n < 2){
            return false;
        }
        for(int i = 2; i <= n / 2; i++){
            if(n % i == 0){
                return false;
            }
        }
        return true;
    }
}

```
