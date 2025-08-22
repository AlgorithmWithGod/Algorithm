```java
import java.io.*;
import java.util.*;

public class Main {

    static int h, w;
    static char[][] map;
    static boolean[][] visited;
    static boolean[] key;
    static List<int[]>[] door;
    static final int[] dr = {-1, 1, 0, 0};
    static final int[] dc = {0, 0, -1, 1};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder out = new StringBuilder();

        int T = Integer.parseInt(br.readLine().trim());
        for(int t=0;t<T;t++){
            StringTokenizer st = new StringTokenizer(br.readLine());
            h = Integer.parseInt(st.nextToken());
            w = Integer.parseInt(st.nextToken());

            map = new char[h + 2][w + 2];
            for (int i = 0; i < h + 2; i++) Arrays.fill(map[i], '.');

            for (int r = 1; r <= h; r++) {
                String line = br.readLine();
                for (int c = 1; c <= w; c++) {
                    map[r][c] = line.charAt(c - 1);
                }
            }

            key = new boolean[26];
            door = new ArrayList[26];
            for (int i = 0; i < 26; i++) door[i] = new ArrayList<>();

            String keys = br.readLine().trim();
            if (!keys.equals("0")) {
                for (int i = 0; i < keys.length(); i++) {
                    char ch = keys.charAt(i);
                    if ('a' <= ch && ch <= 'z') key[ch - 'a'] = true;
                }
            }

            out.append(bfs()).append('\n');
        }

        System.out.print(out.toString());
    }

    static int bfs() {
        visited = new boolean[h + 2][w + 2];
        Deque<int[]> q = new ArrayDeque<>();
        q.offer(new int[]{0, 0});
        visited[0][0] = true;

        int docs = 0;

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int r = cur[0], c = cur[1];

            for (int d = 0; d < 4; d++) {
                int nr = r + dr[d];
                int nc = c + dc[d];

                if (nr < 0 || nr >= h + 2 || nc < 0 || nc >= w + 2) continue;
                if (visited[nr][nc]) continue;

                char ch = map[nr][nc];

                if (ch == '*') continue;

                if ('A' <= ch && ch <= 'Z') {
                    int idx = ch - 'A';
                    if (!key[idx]) {
                        door[idx].add(new int[]{nr, nc});
                        continue;
                    }
                }

                if ('a' <= ch && ch <= 'z') {
                    int idx = ch - 'a';
                    if (!key[idx]) {
                        key[idx] = true;
                        for (int[] pos : door[idx]) {
                            int rr = pos[0], cc = pos[1];
                            if (!visited[rr][cc]) {
                                visited[rr][cc] = true;
                                q.offer(new int[]{rr, cc});
                            }
                        }
                        door[idx].clear();
                    }
                    map[nr][nc] = '.';
                }

                if (ch == '$') {
                    docs++;
                    map[nr][nc] = '.';
                }

                visited[nr][nc] = true;
                q.offer(new int[]{nr, nc});
            }
        }

        return docs;
    }
}

```
