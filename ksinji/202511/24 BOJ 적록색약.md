```java
import java.io.*;
import java.util.*;

public class Main {
    static char[][] map;
    static boolean[][] visited;

    static int[] dy = {-1, 1, 0, 0};
    static int[] dx = {0, 0, -1, 1};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        map = new char[n][n];
        visited = new boolean[n][n];
        
        for (int i=0; i<n; i++){
            String st = br.readLine();
            for (int j=0; j<n; j++){
                map[i][j] = st.charAt(j);
            }
        }

        int count = 0;
        int rgcount = 0;

        for (int i=0; i<n; i++){
            for (int j=0; j<n; j++){
                if (!visited[i][j]){
                    Queue<int[]> queue = new ArrayDeque<>();
                    queue.add(new int[]{i, j});
                    visited[i][j] = true;

                    while (!queue.isEmpty()){
                        int[] cur = queue.poll();

                        for (int k=0; k<4; k++){
                            int nx = cur[0] + dx[k];
                            int ny = cur[1] + dy[k];

                            if (nx < n && nx >= 0 && ny < n && ny >= 0 && !visited[nx][ny]
                                && map[cur[0]][cur[1]] == map[nx][ny]){
                                visited[nx][ny] = true;
                                queue.add(new int[]{nx, ny});

                            }
                        }
                    }
                    count++;
                }
            }
        }

        for (int i=0; i<n; i++){
            Arrays.fill(visited[i], false);
        }

        for (int i=0; i<n; i++){
            for (int j=0; j<n; j++){
                if (!visited[i][j]){
                    Queue<int[]> queue = new ArrayDeque<>();
                    queue.add(new int[]{i, j});
                    visited[i][j] = true;

                    while (!queue.isEmpty()){
                        int[] cur = queue.poll();

                        for (int k=0; k<4; k++){
                            int nx = cur[0] + dx[k];
                            int ny = cur[1] + dy[k];

                            if (nx < n && nx >= 0 && ny < n && ny >= 0 && !visited[nx][ny]
                                && ((map[cur[0]][cur[1]] == 'B' && map[nx][ny] == 'B') || (map[cur[0]][cur[1]] != 'B' && map[nx][ny] != 'B'))){
                                visited[nx][ny] = true;
                                queue.add(new int[]{nx, ny});

                            }
                        }
                    }
                    rgcount++;
                }
            }
        }

        System.out.println(count + " " + rgcount);
    }
}
```
