```java
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int N = 20;
        int[][] arr = new int[N][N];

        // 검사 방향: 아래, 우상향, 좌하향, 우측
        int[] dr = {1, -1, 1, 0};
        int[] dc = {0, 1, 1, 1};

        for (int i = 1; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 1; j < N; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        int winner = 0;
        int winnerR = 0;
        int winnerC = 0;

        for (int r = 1; r < N; r++) {
            for (int c = 1; c < N; c++) {
                
                if (winner > 0) break; // 승부 결정 완료
                if (arr[r][c] == 0) continue;

                // 방향 체크
                for (int i = 0; i < 4; i++) {

                    int cnt = 1; // (r, c)에서 시작, 연속된 바둑돌 개수 카운트
                    int nr = r + dr[i];
                    int nc = c + dc[i];

                    while (1 <= nr && nr < N && 1 <= nc && nc < N) {
                        if (arr[nr][nc] != arr[r][c]) {
                            break;
                        }
                        nr += dr[i];
                        nc += dc[i];
                        cnt++;
                    }

                    // i방향으로 연속된 바둑돌이 5개인 경우
                    if (cnt == 5) {
                        // (r, c) 이전의 바둑돌 색상을 확인하여 6개 이상인지 체크
                        int prevR = r - dr[i];
                        int prevC = c - dc[i];

                        boolean isValid = false;
                        if (1 <= prevR && prevR < N && 1 <= prevC && prevC < N) {
                            if (arr[r][c] != arr[prevR][prevC]) {
                                isValid = true;
                            }
                        }
                        else { // 이전의 바둑돌이 없다면 5개임이 보장
                            isValid = true;
                        }

                        if (isValid) {
                            winner = arr[r][c];
                            winnerR = r;
                            winnerC = c;
                            break; // 승부 결정 완료
                        }
                    }
                }
            }
        }

        bw.write(winner + "\n");
        if (winner > 0) {
            bw.write(winnerR + " " + winnerC);
        }


        br.close();
        bw.flush();
        bw.close();
    }
}

```

- (r, c)에서 ⬇↗↘➡ 방향으로 진행해서 같은 색 바둑돌 5개를 찾은 경우

- 육목일 가능성이 없는지 진행 방향의 반대 방향으로 가서 확인

- `틀렸습니다` 받은 이유
    - 육목 가능성 체크하기 위해 반대 방향의 좌표 (prevR, prevC)룰 구할 때
    - (prevR, prevC)가 범위를 벗어난다면 해당 케이스는 오목임이 보장됨
    - 범위 벗어나는 경우 생각 못하고 `범위 내에 있을때, (r, c)와 같은 색 바둑돌인지`만 체크했던 실수💥

- 가능한 케이스들을 꼼꼼히 생각해 보는 것이 중요