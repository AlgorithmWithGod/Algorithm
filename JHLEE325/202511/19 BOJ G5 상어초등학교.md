```java
import java.io.*;
import java.util.*;

public class Main {

    static int N;
    static int[][] classroom;
    static int[][] likes;
    static int[] dr = {-1, 1, 0, 0};
    static int[] dc = {0, 0, -1, 1};

    public static void main(String[] args) throws Exception {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());

        classroom = new int[N][N];
        likes = new int[N*N + 1][4];

        List<Integer> order = new ArrayList<>();

        for (int i = 0; i < N * N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int student = Integer.parseInt(st.nextToken());
            order.add(student);

            for (int j = 0; j < 4; j++) {
                likes[student][j] = Integer.parseInt(st.nextToken());
            }
        }

        for (int student : order) {
            placeStudent(student);
        }

        System.out.println(calculateScore());
    }

    static void placeStudent(int student) {

        int bestR = -1, bestC = -1;
        int bestLike = -1;
        int bestEmpty = -1;

        for (int r = 0; r < N; r++) {
            for (int c = 0; c < N; c++) {

                if (classroom[r][c] != 0) continue;

                int likeCnt = 0;
                int emptyCnt = 0;

                for (int d = 0; d < 4; d++) {
                    int nr = r + dr[d];
                    int nc = c + dc[d];

                    if (nr < 0 || nc < 0 || nr >= N || nc >= N) continue;

                    if (classroom[nr][nc] == 0) emptyCnt++;
                    else {
                        int other = classroom[nr][nc];
                        if (isLike(student, other)) likeCnt++;
                    }
                }

                if (likeCnt > bestLike ||
                        (likeCnt == bestLike && emptyCnt > bestEmpty) ||
                        (likeCnt == bestLike && emptyCnt == bestEmpty && r < bestR) ||
                        (likeCnt == bestLike && emptyCnt == bestEmpty && r == bestR && c < bestC)) {

                    bestR = r;
                    bestC = c;
                    bestLike = likeCnt;
                    bestEmpty = emptyCnt;
                }
            }
        }

        classroom[bestR][bestC] = student;
    }

    static boolean isLike(int student, int other) {
        for (int x : likes[student]) {
            if (x == other) return true;
        }
        return false;
    }

    static int calculateScore() {
        int score = 0;

        for (int r = 0; r < N; r++) {
            for (int c = 0; c < N; c++) {

                int student = classroom[r][c];
                int likeCnt = 0;

                for (int d = 0; d < 4; d++) {
                    int nr = r + dr[d];
                    int nc = c + dc[d];

                    if (nr < 0 || nc < 0 || nr >= N || nc >= N) continue;

                    int other = classroom[nr][nc];
                    if (isLike(student, other)) likeCnt++;
                }

                if (likeCnt > 0) {
                    score += (int) Math.pow(10, likeCnt - 1);
                }
            }
        }

        return score;
    }
}
```
