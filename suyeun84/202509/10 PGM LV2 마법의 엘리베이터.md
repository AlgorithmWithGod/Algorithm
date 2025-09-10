```java
class Solution {
    public int solution(int storey) {
        int answer = 0;
        while(storey > 0) {
            int temp = storey % 10;
            storey /= 10;
            
            if (temp > 5) {
                answer += (10-temp);
                storey++;
            } else if (temp < 5) {
                answer += temp;
            } else if (storey % 10 >= 5) {
                answer += 5;
                storey++;
            } else {
                answer += 5;
            }
        }
        return answer;
    }
}
```
