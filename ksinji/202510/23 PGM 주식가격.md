```java
class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        
        for(int i = 0; i<prices.length; i++){
            if (prices[i] == 1) {
                answer[i] = prices.length-i-1;
                continue;
            }
            int cnt = 0;
            for (int j=i+1; j<prices.length; j++){
                if (prices[j] < prices[i]) {
                    answer[i] = ++cnt;
                    break;
                }
                else cnt++;
            }
            answer[i] = cnt;
        }
        return answer;
    }
}
```
