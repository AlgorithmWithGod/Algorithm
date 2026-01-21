```java
class Solution {
    public int solution(int n) {
        int answer = n+1;
        int cnt = countOne(n);
        
        while (answer > n) {
            if (countOne(answer) == cnt){
                break;
            }
            answer++;
        }
        
        return answer;
    }
    
    int countOne(int x) {
        String s = Integer.toBinaryString(x);
        int cnt = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '1') cnt++;
        }
        return cnt;
    }
}
```
