```
import java.util.*;

class Solution {
    private String[][] tickets;
    private boolean[] used;
    private List<String> answer;
    private int n;

    public String[] solution(String[][] tickets) {
        this.tickets = tickets;
        this.n = tickets.length;
        this.used = new boolean[n];

        Arrays.sort(this.tickets, (a, b) -> {
            if (!a[0].equals(b[0])) {
                return a[0].compareTo(b[0]);
            }
            return a[1].compareTo(b[1]);
        });

        List<String> path = new ArrayList<>();
        path.add("ICN");

        dfs("ICN", 0, path);

        return answer.toArray(new String[0]);
    }

    private boolean dfs(String current, int count, List<String> path) {
        if (count == n) {
            answer = new ArrayList<>(path);
            return true;
        }

        for (int i = 0; i < n; i++) {
            if (!used[i] && tickets[i][0].equals(current)) {
                used[i] = true;
                path.add(tickets[i][1]);

                if (dfs(tickets[i][1], count + 1, path)) {
                    return true;
                }

                path.remove(path.size() - 1);
                used[i] = false;
            }
        }

        return false;
    }
}
```
