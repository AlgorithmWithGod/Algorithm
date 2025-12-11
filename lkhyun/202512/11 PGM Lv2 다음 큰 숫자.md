```java
class Solution {
    public int solution(int n) {
        int cur = Integer.bitCount(n);
        
        while(true){
            n++;
            if(Integer.bitCount(n) == cur) return n;
        }
    }
}
```
