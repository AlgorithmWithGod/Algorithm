```java
import java.util.*;

class Solution {
    private int maxCount = 0;

    public int solution(int k, int[][] dungeons){
        boolean[] visited = new boolean[dungeons.length];
        dfs(k, dungeons, visited, 0);
        return maxCount;
    }

    private void dfs(int cur, int[][] dungeons, boolean[] visited, int count){
        if(count > maxCount){
            maxCount = count;
        }
        for(int i = 0; i < dungeons.length; i++){
            if(visited[i]) {
                continue;
            }
            int required = dungeons[i][0];
            int cost = dungeons[i][1];
            if(cur < required){
                continue;
            }
            visited[i] = true;
            dfs(cur - cost, dungeons, visited, count + 1);
            visited[i] = false;
        }
    }
}

```
