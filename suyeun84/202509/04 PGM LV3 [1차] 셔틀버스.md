```java
import java.util.*;
class Solution {
    public String solution(int n, int t, int m, String[] timetable) {
        int answer = 0;
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        // 크루 도착 시간
        for (String time : timetable) pq.add(convertToTime(time));
        
        int departTime = 9*60;
        List<List<Integer>> bus = new ArrayList<>();
        // 각 버스에 타는 크루 저장
        for (int i = 0; i < n; i++) bus.add(new ArrayList<>());
        
        for (int i = 0; i < n; i++) {
            while (!pq.isEmpty()) {
                int crew = pq.poll();
                if (bus.get(i).size() < m && crew <= departTime) {
                    bus.get(i).add(crew);
                    answer = crew - 1;
                } else {
                    pq.add(crew);
                    break;
                }
            }
            departTime += t;
        }
        
        if (bus.get(n-1).size() < m) answer = departTime - t;
        return convertToString(answer);
    }
    
    static int convertToTime(String s) {
        String[] a = s.split(":");
        return Integer.parseInt(a[0]) * 60 + Integer.parseInt(a[1]);
    }
    
    static String convertToString(int time) {
        return String.format("%02d:%02d", time / 60, time % 60);
    }
}
```
