```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int[] dx = {-1,1,0,0};
    static int[] dy = {0,0,-1,1};

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());
        for (int t = 0; t < T; t++) {
            st = new StringTokenizer(br.readLine());
            int h = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());
            char[][] map = new char[h][w];

            for (int i = 0; i < h; i++) {
                String line = br.readLine();
                for (int j = 0; j < w; j++) {
                    map[i][j] = line.charAt(j);
                }
            }

            String keyInput = br.readLine();
            Set<Character> keys = new HashSet<>();
            if (!keyInput.equals("0")) {
                for (char c : keyInput.toCharArray()) {
                    keys.add(c);
                }
            }

            int documents = 0;
            while (true) {
                Set<Character> prevKeys = new HashSet<>(keys);

                int[] result = BFS(map, h, w, keys);
                documents = result[0];

                boolean foundNewKey = false;
                for (char key : keys) {
                    if (!prevKeys.contains(key)) {
                        foundNewKey = true;
                        break;
                    }
                }

                if (!foundNewKey) {
                    break;
                }
            }
            bw.write(documents + "\n");
        }
        bw.close();
    }

    static int[] BFS(char[][] map, int h, int w, Set<Character> keys) {
        ArrayDeque<int[]> q = new ArrayDeque<>();
        boolean[][] visited = new boolean[h][w];
        int documents = 0;

        for (int i = 0; i < h; i++) {
            for (int j = 0; j < w; j++) {
                if ((i == 0 || i == h-1 || j == 0 || j == w-1) && map[i][j] != '*') {
                    if (canMove(map[i][j], keys)) {
                        visited[i][j] = true;
                        q.offer(new int[]{i, j});

                        if (map[i][j] == '$') {
                            documents++;
                        } else if (isLowerCase(map[i][j])) {
                            keys.add(map[i][j]);
                        }
                    }
                }
            }
        }

        while (!q.isEmpty()) {
            int[] curr = q.poll();
            int x = curr[0], y = curr[1];

            for (int d = 0; d < 4; d++) {
                int nx = x + dx[d];
                int ny = y + dy[d];

                if (nx < 0 || nx >= h || ny < 0 || ny >= w || visited[nx][ny]) {
                    continue;
                }

                char cell = map[nx][ny];

                if (canMove(cell, keys)) {
                    visited[nx][ny] = true;
                    q.offer(new int[]{nx, ny});

                    if (cell == '$') {
                        documents++;
                    } else if (isLowerCase(cell)) {
                        keys.add(cell);
                    }
                }
            }
        }

        return new int[]{documents};
    }

    static boolean canMove(char cell, Set<Character> keys) {
        if (cell == '*') return false;
        if (cell == '.' || cell == '$') return true;
        if (isLowerCase(cell)) return true;
        if (isUpperCase(cell)) {
            return keys.contains(Character.toLowerCase(cell));
        }
        return false;
    }

    static boolean isUpperCase(char c) {
        return c >= 'A' && c <= 'Z';
    }

    static boolean isLowerCase(char c) {
        return c >= 'a' && c <= 'z';
    }
}
```
