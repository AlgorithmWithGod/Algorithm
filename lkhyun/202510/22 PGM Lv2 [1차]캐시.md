```java
import java.util.*;
class Solution {
    public int solution(int cacheSize, String[] cities) {
        int answer = 0;
        List<String> cache = new LinkedList<>();
        
        for(String c : cities){
            String city = c.toLowerCase();
            if(cache.contains(city)){
                cache.remove(city);
                cache.add(city);
                answer++;
            }else{
                cache.add(city);
                answer+=5;
            }
            if(cache.size() > cacheSize){
                cache.remove(0);
            }
        }
        return answer;
    }
}
```
