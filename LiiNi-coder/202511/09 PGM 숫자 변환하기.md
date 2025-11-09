```java
import java.util.*;

class Solution {
    private static int MAX = 1_000_001;
    public int solution(int x, int y, int n) {
        int answer = 0;
        Queue<int[]> q = new ArrayDeque<int[]>();
        q.offer(new int[]{0, x});
        boolean[] visited = new boolean[MAX];
        visited[x] = true;
        boolean hasAnswer = false;
        int count = 0, value;
        while(!q.isEmpty()){
            int[] temp = q.poll();
            count = temp[0];
            value = temp[1];
            if(value == y){
                hasAnswer = true;
                break;
            }
            for(int new_value: new int[]{value+n, value*2, value*3}){
                if(new_value >= MAX){
                    continue;
                }
                if(visited[new_value])
                    continue;
                q.offer(new int[]{count+1, new_value});
                visited[new_value] = true;
            }
            
        }
        return (hasAnswer)? count: -1;
    }
}
```
