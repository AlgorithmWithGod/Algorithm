```
import java.util.*;

class Solution {
    static String[][] tickets;
    static List<String> answer = new ArrayList<>();
    static int n;
    static boolean[] visited;
    
    public String[] solution(String[][] stickets) {
        tickets = stickets;
        n = tickets.length;
        visited = new boolean[n];
        
        dfs(0, "ICN", "ICN");
        Collections.sort(answer);
        
        return answer.get(0).split(",");
    }
    public static void dfs(int depth, String start, String path) {
            if (depth == n) {
                answer.add(path);
                return;
            }
            for (int i = 0; i < tickets.length; i++) {
                if (tickets[i][0].equals(start) && !visited[i]) {
                    visited[i] = true;
                    dfs(depth+1, tickets[i][1], path + ","+tickets[i][1]);
                    visited[i] = false;
                    
                }
            }
        }
}
```
