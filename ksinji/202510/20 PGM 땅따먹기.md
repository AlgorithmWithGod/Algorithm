```java
class Solution {
    public int solution(int[][] land) {
        int n = land.length;
        int a = land[0][0], b = land[0][1], c = land[0][2], d = land[0][3];

        for (int i = 1; i < n; i++) {
            int na = land[i][0] + Math.max(Math.max(b, c), d);
            int nb = land[i][1] + Math.max(Math.max(a, c), d);
            int nc = land[i][2] + Math.max(Math.max(a, b), d);
            int nd = land[i][3] + Math.max(Math.max(a, b), c);
            a = na; b = nb; c = nc; d = nd;
        }
        return Math.max(Math.max(a, b), Math.max(c, d));
    }
}
```
