```java
class Solution {
    static final int REMAINDER = 1234567;
    
    public int solution(int n) {
        int[] fibo = new int[100001];
        fibo[1] = 1;
        
        for (int i = 2; i <= 100000; i++){
            fibo[i] = fibo[i-1] + fibo[i-2];
            fibo[i] %= REMAINDER;
        }
        
        int answer = fibo[n];
        
        return answer;
    }
}
```
