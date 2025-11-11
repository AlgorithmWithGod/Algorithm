```java
class Solution {
    public int solution(int[] money) {
        int n = money.length;
        
        int A0 = 0;
        int A1 = 0;

        int B0 = 0;
        int B1 = money[0];

        for (int i = 1; i < n; i++) {
            int newA0 = Math.max(A0, A1);
            int newA1 = A0 + money[i];
            A0 = newA0; A1 = newA1;

            if (i <= n - 2) {
                int newB0 = Math.max(B0, B1);
                int newB1 = B0 + money[i];
                B0 = newB0; B1 = newB1;
            }
        }

        int bestA = Math.max(A0, A1);
        int bestB = Math.max(B0, B1);
        return Math.max(bestA, bestB);
    }
}
```
