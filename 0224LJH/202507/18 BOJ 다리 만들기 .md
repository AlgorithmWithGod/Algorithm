```java
import java.awt.*;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static int[][] arr;
    static boolean[][] visited;
    static int[] dy = {-1,0,1,0};
    static int[] dx = {0,1,0,-1};
    static int size;
    static final int LAND = 1;
    static final int WATER = 0;

    public static void main(String[] args) throws IOException {
        init();
        int result = process();
        System.out.println(result);
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        size = Integer.parseInt(br.readLine());
        arr = new int[size][size];

        for (int i = 0; i < size; i++){
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < size; j++){
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }
    }

    private static int process() {
        // 모든 섬들을 서로 다른 번호로 표시
        visited = new boolean[size][size];
        int islandNum = 2;

        for (int i = 0; i < size; i++){
            for (int j = 0; j < size; j++){
                if (arr[i][j] == LAND && !visited[i][j]){
                    markIsland(i, j, islandNum);
                    islandNum++;
                }
            }
        }

        // 각 섬에서 다른 섬으로 가는 최단 거리 찾기
        int minDistance = Integer.MAX_VALUE;

        for (int currentIsland = 2; currentIsland < islandNum; currentIsland++) {
            int distance = bfsFromIsland(currentIsland);
            minDistance = Math.min(minDistance, distance);
        }

        return minDistance;
    }

    private static void markIsland(int y, int x, int islandNum) {
        Queue<Point> q = new LinkedList<>();
        arr[y][x] = islandNum;
        q.add(new Point(x, y));
        visited[y][x] = true;

        while (!q.isEmpty()){
            Point p = q.poll();
            for (int i = 0; i < 4; i++) {
                int nx = p.x + dx[i];
                int ny = p.y + dy[i];
                if (ny < 0 || ny >= size || nx < 0 || nx >= size) continue;
                if (visited[ny][nx] || arr[ny][nx] != LAND) continue;

                visited[ny][nx] = true;
                arr[ny][nx] = islandNum;
                q.add(new Point(nx, ny));
            }
        }
    }

    private static int bfsFromIsland(int startIsland) {
        Queue<Point> queue = new LinkedList<>();
        boolean[][] bfsVisited = new boolean[size][size];

        // 시작 섬의 모든 셀을 큐에 추가
        for (int i = 0; i < size; i++){
            for (int j = 0; j < size; j++){
                if (arr[i][j] == startIsland){
                    queue.add(new Point(j, i));
                    bfsVisited[i][j] = true;
                }
            }
        }

        int distance = 0;

        while (!queue.isEmpty()) {
            int qSize = queue.size();

            for (int i = 0; i < qSize; i++) {
                Point p = queue.poll();

                for (int k = 0; k < 4; k++) {
                    int nx = p.x + dx[k];
                    int ny = p.y + dy[k];

                    if (nx < 0 || ny < 0 || nx >= size || ny >= size) continue;
                    if (bfsVisited[ny][nx]) continue;

                    // 다른 섬을 찾았다면 거리 반환
                    if (arr[ny][nx] >= 2 && arr[ny][nx] != startIsland) {
                        return distance;
                    }

                    // 물이면 다음 레벨로 확장
                    if (arr[ny][nx] == WATER) {
                        bfsVisited[ny][nx] = true;
                        queue.add(new Point(nx, ny));
                    }
                }
            }
            distance++;
        }

        return Integer.MAX_VALUE;
    }
}


```
