```java
import java.util.*;

class Solution {
    private static HashMap<String, Integer> wordsIndex;

    public int solution(String[] wants, int[] number, String[] discounts) {
        int answer = 0;
        wordsIndex = new HashMap<String, Integer>();
        int i = 0;
        for(String want : wants){
            wordsIndex.put(want, i++);
        }
        int[] counts = new int[wants.length];
        
        ArrayDeque<String> q = new ArrayDeque<String>();
        String polled;
        for(String discount : discounts){
            if(wordsIndex.containsKey(discount)){
                counts[wordsIndex.get(discount)]++;
            }
            q.offer(discount);
            if(q.size() > 10){
                polled = q.poll();
                if(wordsIndex.containsKey(polled)){
                    counts[wordsIndex.get(polled)]--;
                }
            }

            if(q.size() == 10){
                boolean ok = true;
                for(int k=0; k<number.length; k++){
                    if(counts[k] < number[k]){
                        ok = false;
                        break;
                    }
                }
                if(ok){
                    answer++;
                }
            }
        }

        return answer;
    }
}

```
