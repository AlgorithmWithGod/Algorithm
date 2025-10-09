```java
class Solution {
    public int solution(int n) {
        int[] sum = new int[n + 1];
        for(int i=1; i<=n; i++)
            sum[i] = sum[i-1] + i;

        int l = 0, r = 1, answer = 0;
        while(l < r && r <= n){
            int now = sum[r] - sum[l];
            if(now == n){
                answer++;
                r++;
            }else if(now < n)
                r++;
            else
                l++;
        }
        
        return answer;
    }
}
```
