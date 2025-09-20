```java
import java.io.*;
import java.util.*;

public class Main {
    static int n;
    static int[] arr;
    static boolean[] visited;
    static int answer = 0;
    static int[] indegree;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(br.readLine());
        while(t-- > 0){
            n = Integer.parseInt(br.readLine());
            arr = new int[n + 1];
            visited = new boolean[n + 1];
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int i = 1; i <= n; i++) {
                arr[i] = Integer.parseInt(st.nextToken());
            }

            for (int i = 1; i <= n; i++) {
                if (!visited[i]) {
                    dfs(i);
                }
            }

            System.out.println(n - answer);
        }

    }

    static void dfs(int start) {
        Map<Integer, Integer> map = new HashMap<>();
        List<Integer> path = new ArrayList<>();

        int cur = start;
        while (true) {
            if (visited[cur]) {
                break;
            }

            visited[cur] = true;
            map.put(cur, path.size());
            path.add(cur);
            int next = arr[cur];
            //다음 학생이 범위를 벗어나면 즉시 종료(ㅣ사이클 없으니까)
            if (next < 1 || next > n) break;

            if (!map.containsKey(next)) {
                cur = next;
                continue;
            } else {
                //사이클 발견
                int idx = map.get(next);
                answer += path.size() - idx;
                break;
            }
        }
    }
}

```
