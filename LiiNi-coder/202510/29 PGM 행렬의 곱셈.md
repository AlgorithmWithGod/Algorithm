```java
import java.util.*;

class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        int rows = arr1.length;
        int cols = arr2[0].length;
        int common = arr2.length;
        int[][] answer = new int[rows][cols];

        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
                int sum = 0;
                for(int k = 0; k < common; k++){
                    sum += arr1[i][k] * arr2[k][j];
                }
                answer[i][j] = sum;
            }
        }

        return answer;
    }
}
```
