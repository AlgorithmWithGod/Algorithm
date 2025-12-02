```
class Solution {
    static final int FULL_CIRCLE = 43200;
    
    public int solution(int h1, int m1, int s1, int h2, int m2, int s2) {
        int start = h1 * 3600 + m1 * 60 + s1;
        int end = h2 * 3600 + m2 * 60 + s2;
        
        int answer = countAlarms(end) - countAlarms(start);
        
        if (isExactOverlap(start)) {
            answer++;
        }
        
        return answer;
    }
    
    private int countAlarms(int time) {
        int mCount = time * 59 / 3600;
        int hCount = time * 719 / 43200;

        int overlap = time / 43200;
        
        return mCount + hCount - overlap;
    }
    
    private boolean isExactOverlap(int time) {
        if (time % 43200 == 0) {
            return true;
        }
        
        double secondAngle = (time % 60) * 6.0;
        double minuteAngle = (time % 3600) * 0.1;
        double hourAngle = (time % 43200) * (1.0 / 120.0);
        
        return Math.abs(secondAngle - minuteAngle) < 0.01 || 
               Math.abs(secondAngle - hourAngle) < 0.01;
    }
}
```
