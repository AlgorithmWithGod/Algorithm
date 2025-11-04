```java
import java.util.*;

class Solution {
    public int[] solution(String msg) {
        List<Integer> answer = new ArrayList<>();
        Map<String, Integer> dictionary = new HashMap<>();
        for(int i = 1; i <= 26; i++){
            dictionary.put(String.valueOf((char)(64 + i)), i);
        }
        int dictionaryIdx = 27;
        
        int cur = 0;
        while(cur < msg.length()){
            String w = String.valueOf(msg.charAt(cur));
            
            while(cur + w.length() < msg.length() && 
                  dictionary.containsKey(w + msg.charAt(cur + w.length()))){
                w = w + msg.charAt(cur + w.length());
            }
            answer.add(dictionary.get(w));
            
            if(cur + w.length() < msg.length()){
                String wc = w + msg.charAt(cur + w.length());
                dictionary.put(wc, dictionaryIdx++);
            }
            
            cur += w.length();
        }
        
        return answer.stream().mapToInt(Integer::intValue).toArray();
    }
}
```
