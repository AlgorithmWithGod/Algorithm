```java
import java.util.*;
class Solution {
    static int toInt(String num) {return Integer.parseInt(num);}
    public String[] solution(String[][] plans) {
        int len = plans.length;
        ArrayList<String> answer = new ArrayList<>();
        Stack<Work> stack = new Stack<>();
        Arrays.sort(plans, (a, b) -> {
            if (a[1].compareTo(b[1]) == 0) return a[2].compareTo(b[2]);
            return a[1].compareTo(b[1]);
        });
        for (int i = 0; i < len-1; i++) {
            String work = plans[i][0];
            int cEndTime = toMinutes(plans[i][1]) + Integer.parseInt(plans[i][2]);
            int nStartTime = toMinutes(plans[i + 1][1]);
            
            if (cEndTime > nStartTime) {
                stack.push(new Work(work, cEndTime - nStartTime));
            } else {
                int leftTime = nStartTime - cEndTime;
                answer.add(work);
                while (leftTime > 0 && !stack.isEmpty()) {
                    Work w = stack.pop();
                    if (w.time > leftTime) {
                        stack.push(new Work(w.work, w.time - leftTime));
                        break;
                    } else if (w.time == leftTime) {
                        answer.add(w.work);
                        break;
                    } else {
                        leftTime -= w.time;
                        answer.add(w.work);
                    }
                }
            }
        }
        answer.add(plans[len-1][0]);
        while(!stack.isEmpty()) {
            answer.add(stack.pop().work);
        }
        return answer.toArray(new String[0]);
    }
    
    private int toMinutes(String time) {
        String[] parts = time.split(":");
        return Integer.parseInt(parts[0]) * 60 + Integer.parseInt(parts[1]);
    }
    
    static class Work {
        String work;
        int time;
        public Work(String work, int time) {
            this.work = work;
            this.time = time;
        }
    }
}
```
