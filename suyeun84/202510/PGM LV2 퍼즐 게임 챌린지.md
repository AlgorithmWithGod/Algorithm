```java
class Solution {
    public int solution(int[] diffs, int[] times, long limit) {
        int answer = 0;
        int start = 1;
        int end = 300000;
        while (start < end) {
            int mid = (start + end) / 2;
            long time = 0;
            for (int i = 0; i < diffs.length; i++) {
                if (diffs[i] <= mid) time += times[i];
                else {
                    int wrong = diffs[i] - mid;
                    if (i == 0) time += (times[0] * wrong + times[i]);
                    else time += ((times[i]+times[i-1]) * wrong + times[i]);
                }
            }
            if (time <= limit) end = mid;
            else start = mid + 1;
        }
        return start;
    }
}
```
