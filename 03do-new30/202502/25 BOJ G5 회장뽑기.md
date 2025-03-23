```java
import java.io.*;
import java.util.*;
public class Main {

   static final int INF = 50;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        // 입력
        int n = Integer.parseInt(br.readLine());

        int[][] dist = new int[n+1][n+1];
        for (int i = 1; i < n+1; i++) {
            for (int j = 1; j < n+1; j++) {
                if (i == j) {
                    continue;
                }
                dist[i][j] = INF;
            }
        }

        while (true) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            if (u == -1 && v == -1) { break; }
            dist[u][v] = 1;
            dist[v][u] = 1;
        }
        
        // 풀이
        for (int mid = 1; mid < n+1; mid++) {
            for (int i = 1; i < n+1; i++) {
                for (int j = 1; j < n+1; j++) {
                    if (i == j) { continue; }
                    dist[i][j] = Integer.min(dist[i][j], dist[i][mid] + dist[mid][j]);
                }
            }
        }

        int[] score = new int[n+1];
        for (int i = 1; i < n+1; i++) {
            score[i] = Arrays.stream(dist[i]).max().getAsInt();
        }
        int minScore = INF;
        int count = 0;
        for (int i = 1; i < n+1; i++) {
            if (score[i] < minScore) {
                minScore = score[i];
                count = 1;
            } else if (score[i] == minScore) {
                count++;
            }
        }
        
        // 출력
        System.out.println(minScore + " " + count);
        for (int i = 1; i < n+1; i++) {
            if (score[i] == minScore) {
                System.out.print(i + " ");
            }
        }
        System.out.println();

        br.close();
    }
}

```
