```java
import java.io.*;
import java.util.*;

public class Main {
    static int n;
    static int[] people;
    static List<Integer>[] graph;
    static boolean[] selected;
    static int res;
    static int INF = 987654321;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        n = Integer.parseInt(br.readLine());
        people = new int[n + 1];
        graph = new ArrayList[n + 1];
        selected = new boolean[n + 1];

        res = INF;

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= n; i++) {
            people[i] = Integer.parseInt(st.nextToken());
            graph[i] = new ArrayList<>();
        }

        for (int i = 1; i <= n; i++) {
            st = new StringTokenizer(br.readLine());
            int cnt = Integer.parseInt(st.nextToken());
            for (int j = 0; j < cnt; j++) {
                graph[i].add(Integer.parseInt(st.nextToken()));
            }
        }

        dfs(1);
        if(res==INF){
            System.out.println(-1);
        }
        else{
            System.out.println(res);
        }
    }

    static void dfs(int idx) {
        if (idx == n + 1) {
            List<Integer> a = new ArrayList<>();
            List<Integer> b = new ArrayList<>();

            for (int i = 1; i <= n; i++) {
                if (selected[i]) a.add(i);
                else b.add(i);
            }

            if (a.isEmpty() || b.isEmpty()) return;

            if (checked(a) && checked(b)) {
                int diff = Math.abs(sum(a) - sum(b));
                res = Math.min(res, diff);
            }
            return;
        }

        selected[idx] = true;
        dfs(idx + 1);

        selected[idx] = false;
        dfs(idx + 1);
    }

    static boolean checked(List<Integer> area) {
        if (area.isEmpty()) return false;

        Queue<Integer> q = new LinkedList<>();
        boolean[] visited = new boolean[n + 1];
        q.add(area.get(0));
        visited[area.get(0)] = true;
        int cnt = 1;

        while (!q.isEmpty()) {
            int now = q.poll();
            for (int next : graph[now]) {
                if (!visited[next] && area.contains(next)) {
                    visited[next] = true;
                    q.add(next);
                    cnt++;
                }
            }
        }

        return cnt == area.size();
    }

    static int sum(List<Integer> area) {
        int s = 0;
        for (int x : area) s += people[x];
        return s;
    }
}
```
