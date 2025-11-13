```java
import java.util.*;

class Solution {
    public int[] solution(int[] fees, String[] records) {
        Map<String, Integer> totalTime = new HashMap<>();
        Map<String, String> inTime = new HashMap<>();

        for (String record : records) {
            String[] parts = record.split(" ");
            String time = parts[0];
            String car = parts[1];
            String type = parts[2];

            if (type.equals("IN")) {
                inTime.put(car, time);
            } else {
                int diff = getTimeDiff(inTime.get(car), time);
                totalTime.put(car, totalTime.getOrDefault(car, 0) + diff);
                inTime.remove(car);
            }
        }

        for (Map.Entry<String, String> entry : inTime.entrySet()) {
            int diff = getTimeDiff(entry.getValue(), "23:59");
            totalTime.put(entry.getKey(), totalTime.getOrDefault(entry.getKey(), 0) + diff);
        }

        TreeMap<String, Integer> result = new TreeMap<>();
        for (Map.Entry<String, Integer> entry : totalTime.entrySet()) {
            int time = entry.getValue();
            int fee = fees[1];
            if (time > fees[0]) {
                fee += (int)Math.ceil((time - fees[0]) / (double)fees[2]) * fees[3];
            }
            result.put(entry.getKey(), fee);
        }

        int[] answer = new int[result.size()];
        int i = 0;
        for (int fee : result.values()) {
            answer[i++] = fee;
        }

        return answer;
    }

    private static int getTimeDiff(String start, String end) {
        String[] s = start.split(":");
        String[] e = end.split(":");
        int startMin = Integer.parseInt(s[0]) * 60 + Integer.parseInt(s[1]);
        int endMin = Integer.parseInt(e[0]) * 60 + Integer.parseInt(e[1]);
        return endMin - startMin;
    }
}

```
