```java
import java.io.*;
import java.util.*;

public class Main {

    final static int INF = 501;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        // [start] 입출력
        int N = Integer.parseInt(st.nextToken()); // 정점의 개수
        int M = Integer.parseInt(st.nextToken()); // 엣지의 개수

        int[][] dist = new int[N+1][N+1];
        for (int i = 0; i < N+1; i++) {
            for (int j = 0; j < N+1; j++) {
                if (i == j) { dist[i][j] = 0; continue;} // 자기 자신으로 가는 비용 0
                dist[i][j] = INF; // 초기값: 도달할 수 없음으로 설정
            }
        }
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            dist[u][v] = 1;
        }
        // [end] 입출력

        // Floyd-Warshall
        for (int mid = 1; mid < N+1; mid++) {
            for (int start = 1; start < N+1; start++) {
                for (int end = 1; end < N+1; end++) {
                    dist[start][end] = Integer.min(dist[start][end], dist[start][mid] + dist[mid][end]);
                }
            }
        }
        int answer = 0;
        for (int target = 1; target < N+1; target++) {
            int lower = 0;
            int higher = 0;
            for (int k = 1; k < N+1; k++) {
                if (target == k) { continue; } // 자기 자신과의 경로는 패스
                if (dist[k][target] != INF) {
                    lower++;
                }
                if (dist[target][k] != INF) {
                    higher++;
                }
            }
            if (lower + higher == N-1) {
                answer++;
            }
        }
        System.out.println(answer);

        br.close();
    }
}

```
