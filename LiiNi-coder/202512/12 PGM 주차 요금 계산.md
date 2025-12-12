```java
import java.util.*;
import java.io.*;

class Solution {
    public int[] solution(int[] fees, String[] records) {
        Map<String, Integer> totalTime = new TreeMap<>();
        Map<String, Integer> inTime = new HashMap<>();

        for(String record : records){
            String[] parts = record.split(" ");
            int hh = Integer.parseInt(parts[0].substring(0, 2));
            int mm = Integer.parseInt(parts[0].substring(3, 5));
            int time = hh * 60 + mm;
            
            String car = parts[1];
            String type = parts[2];
            if(type.equals("IN")){
                inTime.put(car, time);
            } else {
                int start = inTime.remove(car);
                int duration = time - start;
                
                totalTime.put(car, totalTime.getOrDefault(car, 0) + duration);
            }
        }
        for(String car : inTime.keySet()){
            int start = inTime.get(car);
            int end = 23 * 60 + 59;
            int duration = end - start;
            totalTime.put(car, totalTime.getOrDefault(car, 0) + duration);
        }
        
        
        List<Integer> answerList = new ArrayList<>();
        int basicTime = fees[0];
        int basicFee = fees[1];
        int unitTime = fees[2];
        int unitFee = fees[3];

        for(int time : totalTime.values()){
            if(time <= basicTime){
                answerList.add(basicFee);
            } else {
                int extra = time - basicTime;
                int count = extra / unitTime;
                if(extra%unitTime != 0){
                    count++;
                }
                answerList.add(basicFee + count * unitFee);
            }
        }
        int[] answer = new int[answerList.size()];
        for(int i = 0; i < answerList.size(); i++){
            answer[i] = answerList.get(i);
        }

        return answer;
    }
}

```
