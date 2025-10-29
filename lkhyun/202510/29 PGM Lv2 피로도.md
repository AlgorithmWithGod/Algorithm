```java
class Solution {
    static int max = 0;
    public int solution(int k, int[][] dungeons) {
        boolean[] visited = new boolean[dungeons.length];
        backtracking(dungeons, visited, 0, k);
        return max;
    }
    public void backtracking(int[][] dungeons, boolean[] visited, int cnt, int k){
        for(int i = 0; i<dungeons.length; i++){
            if(!visited[i]){
                if(k < dungeons[i][0]) continue;
                visited[i] = true;
                backtracking(dungeons,visited,cnt+1,k-dungeons[i][1]);
                visited[i] = false;
            }
        }
        max = Math.max(max,cnt);
    }
}
```
