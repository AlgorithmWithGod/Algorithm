```java
import java.util.*;
import java.io.*;

public class Main{
    static class Shark{
        int speed;
        int direction;
        int size;

        Shark(int speed, int direction, int size){
            this.speed = speed;
            this.direction = direction;
            this.size = size;
        }
    }

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static int R, C, M;
    static Shark[][] sharks;
    static int ans = 0;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        R = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        sharks = new Shark[R+1][C+1];

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int r = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());
            int s = Integer.parseInt(st.nextToken());
            int d = Integer.parseInt(st.nextToken());
            int z = Integer.parseInt(st.nextToken());

            sharks[r][c] = new Shark(s, d, z);
        }

        // 낚시왕이 오른쪽으로 한 칸씩 이동하면서 상어 잡기
        for (int col = 1; col <= C; col++) {
            ans += catchShark(col);
            sharkMove();
        }

        bw.write(ans + "\n");
        bw.flush();
        bw.close();
    }

    static int catchShark(int col){
        for (int i = 1; i <= R; i++) {
            if(sharks[i][col] != null){
                int size = sharks[i][col].size;
                sharks[i][col] = null;
                return size;
            }
        }
        return 0;
    }

    static void sharkMove(){
        Shark[][] newSharks = new Shark[R+1][C+1];

        for (int i = 1; i <= R; i++) {
            for (int j = 1; j <= C; j++) {
                if(sharks[i][j] != null){
                    Shark shark = sharks[i][j];
                    int[] next = nextState(i, j, shark.speed, shark.direction);
                    int ni = next[0];
                    int nj = next[1];
                    int nd = next[2];

                    if(newSharks[ni][nj] == null || newSharks[ni][nj].size < shark.size){
                        newSharks[ni][nj] = new Shark(shark.speed, nd, shark.size);
                    }
                }
            }
        }
        sharks = newSharks;
    }

    static int[] nextState(int row, int col, int speed, int direction){
        int nextRow = row;
        int nextCol = col;
        int nextDirection = direction;

        if(direction == 1){ // 위
            int restShift = speed % ((R-1) * 2);
            if(restShift >= nextRow - 1){
                restShift -= (nextRow - 1);
                nextDirection = 2;
                nextRow = 1;

                if(restShift >= R - 1){
                    restShift -= (R - 1);
                    nextDirection = 1;
                    nextRow = R;
                }
            }

            if(nextDirection == 1){
                nextRow -= restShift;
            } else {
                nextRow += restShift;
            }

        } else if(direction == 2){ // 아래
            int restShift = speed % ((R-1) * 2);
            if(restShift >= R - nextRow){
                restShift -= (R - nextRow);
                nextDirection = 1;
                nextRow = R;

                if(restShift >= R - 1){
                    restShift -= (R - 1);
                    nextDirection = 2;
                    nextRow = 1;
                }
            }

            if(nextDirection == 1){
                nextRow -= restShift;
            } else {
                nextRow += restShift;
            }

        } else if(direction == 3){ // 오른쪽
            int restShift = speed % ((C-1) * 2);
            if(restShift >= C - nextCol){
                restShift -= (C - nextCol);
                nextDirection = 4;
                nextCol = C;

                if(restShift >= C - 1){
                    restShift -= (C - 1);
                    nextDirection = 3;
                    nextCol = 1;
                }
            }

            if(nextDirection == 3){
                nextCol += restShift;
            } else {
                nextCol -= restShift;
            }

        } else if(direction == 4){ // 왼쪽
            int restShift = speed % ((C-1) * 2);
            if(restShift >= nextCol - 1){
                restShift -= (nextCol - 1);
                nextDirection = 3;
                nextCol = 1;

                if(restShift >= C - 1){
                    restShift -= (C - 1);
                    nextDirection = 4;
                    nextCol = C;
                }
            }

            if(nextDirection == 3){
                nextCol += restShift;
            } else {
                nextCol -= restShift;
            }
        }

        return new int[]{nextRow, nextCol, nextDirection};
    }
}
```
