```java
import java.util.*;
class Solution {
    static int toInt(String s) {return Integer.parseInt(s);}
    
    public int solution(String[][] book_time) {
        int answer = 0;
        int len = book_time.length;
        if (len == 1) return 1;
        Arrays.sort(book_time, (a, b) -> a[0].compareTo(b[0]));

        PriorityQueue<Integer> q = new PriorityQueue<>();
        String[] e = book_time[0][1].split(":");
        q.add(toInt(e[0])*60 + toInt(e[1]));
        
        int idx = 1;
        while (!q.isEmpty()) {
            int curr = q.peek();
            String[] start = book_time[idx][0].split(":");
            String[] end = book_time[idx][1].split(":");

            int sMin = toInt(start[0])*60 + toInt(start[1]);
            int eMin = toInt(end[0])*60 + toInt(end[1]);
            if (curr + 10 <= sMin) q.poll();
            q.add(eMin);
            idx++;
            if (idx >= len) break;
        }

        return q.size();
    }
}
```
