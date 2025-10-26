```java
class Solution {
    static boolean[] visited;
    static int answer = 0;

    public int solution(int k, int[][] dungeons) {
        visited = new boolean[dungeons.length];
        dfs(k, dungeons, 0);
        return answer;
    }

    static void dfs(int now, int[][] dungeons, int count) {
        if (count > answer) answer = count;

        for (int i = 0; i < dungeons.length; i++) {
            if (visited[i]) continue;

            int need = dungeons[i][0];
            int cost = dungeons[i][1];

            if (now >= need) {
                visited[i] = true;
                dfs(now - cost, dungeons, count + 1);
                visited[i] = false;
            }
        }
    }
}
```
