```java
import java.util.*;

public class Main {
    static int[] dr = {0, 0, -1, 1};
    static int[] dc = {-1, 1, 0, 0};
    static int answer;
    static char[][] arr;
    static int[] girls;
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        arr = new char[5][5];
        for (int i = 0; i < 5; i++) {
            arr[i] = sc.next().toCharArray();
        }
        girls = new int[7];
        solve(0, 0, 0);
        System.out.println(answer);
        sc.close();
    }

    static void solve(int idx, int start, int sCount) {
        if (idx == 7) {
            if (sCount >= 4 && isValidGirls()) { answer++; }
            return;
        }

        for (int i = start; i < 25; i++) {
            int r = i / 5;
            int c = i % 5;

            girls[idx] = i;
            if (arr[r][c] == 'S') {
                solve(idx + 1, i + 1, sCount + 1);
            } else {
                solve(idx + 1, i + 1, sCount);
            }
        }
    }

    static boolean isValidGirls() {
        Queue<Integer> q = new ArrayDeque<>();
        boolean[] visited = new boolean[25];
        q.offer(girls[0]);
        visited[girls[0]] = true;
        while (!q.isEmpty()) {
            int x = q.poll();
            int r = x / 5;
            int c = x % 5;
            for (int i = 0; i < 4; i++) {
                int nr = r + dr[i];
                int nc = c + dc[i];
                int y = nr * 5 + nc;
                if (nr < 0 || nr >= 5 || nc < 0 || nc >= 5) { continue; }
                if (visited[y]) { continue; }
                // girls에 포함된 경우에만 방문 표시
                for (int idx = 0; idx < 7; idx++) {
                    if (girls[idx] == y) {
                        visited[y] = true;
                        q.offer(y);
                        break;
                    }
                }
            }
        }
        for (int girl : girls) {
            if (!visited[girl]) { return false;}
        }
        return true;

    }
}
```
