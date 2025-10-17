```java
import java.util.*;

class Solution {
    public int solution(int[] queue1, int[] queue2) {
        int n = queue1.length;
        int totalSize = n*2;

        long queueValue = 0, totalValue = 0;
        int[] nums = new int[totalSize];

        for (int i = 0; i < n; i++) {
            nums[i] = queue1[i];
            queueValue += queue1[i];
            totalValue  += queue1[i];
        }
        for (int i = 0; i < n; i++) {
            nums[n + i] = queue2[i];
            totalValue += queue2[i];
        }

        // 전체 합이 홀수면 불가능
        if (totalValue % 2 == 1) return -1;
        long half = totalValue / 2;

        if (queueValue == half) return 0;

        int i = 0;      // q1 시작 위치
        int j = n;      // q2 시작 위치
        int moves = 0;

        // 각 포인터는 최대 L까지 갈 수 있음
        while (i < totalSize && j < totalSize) {
            if (queueValue == half) return moves;

            if (queueValue > half) {
                queueValue -= nums[i++];
            } else {
                queueValue += nums[j++];
            }
            moves++;
        }
        return -1;
    }
}
```
