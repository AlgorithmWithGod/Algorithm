```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int ans = 0;

    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        int[][] board = new int[N][N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                board[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        backtracking(0, board);

        bw.write(ans +"");
        bw.close();
    }
    static void backtracking(int moveCnt, int[][] board) throws IOException {
        if(moveCnt == 10) {
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < N; j++) {
                    ans = Math.max(ans, board[i][j]);
                }
            }
            return;
        }
        int max = 0;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                max = Math.max(max, board[i][j]);
            }
        }
        if(max * (1<<(10 - moveCnt)) <= ans) return;
        for (int k = 1; k <= 4; k++) {
            int[][] newBoard = new int[N][N];
            for (int i = 0; i < N; i++) {
                System.arraycopy(board[i], 0, newBoard[i], 0, N);
            }
            move(k, newBoard);
            backtracking(moveCnt + 1, newBoard);
        }
    }
    static void move(int opt, int[][] board){ //1이면 위, 2면 아래, 3이면 왼쪽, 4면 오른쪽
        boolean[][] visited = new boolean[N][N];
        if(opt == 1) {
            for (int i = 1; i < N; i++) {
                for (int j = 0; j < N; j++) {
                    if(board[i][j] == 0) { //빈칸이면 넘어감
                        continue;
                    }
                    int tmp = i-1; //tmp는 현재 칸과 마주할 칸을 나타냄
                    while(tmp >= 0 && board[tmp][j]==0){ //바로 윗칸이 빈칸이 아닐때까지 이동
                        tmp--;
                    }
                    if(tmp<0){// 현재 칸 위가 다 빈칸일 경우
                        board[0][j] = board[i][j]; //맨 윗칸에 현재칸 두고 끝
                        board[i][j] = 0;
                        continue;
                    }
                    if(board[i][j] == board[tmp][j] && !visited[tmp][j]){ //충돌시 같고 이미 합쳐진 블록이 아닐경우
                        board[tmp][j] *= 2;
                        visited[tmp][j] = true;
                        board[i][j] = 0;
                    }else{ //다르다면 tmp 한칸 앞에 그냥 둠
                        board[tmp+1][j] = board[i][j];
                        if(tmp+1 != i){ //tmp가 애초에 i랑 딱 붙어있을 경우에는 그대로가 유지되게 함.
                            board[i][j] = 0;
                        }
                    }
                }
            }
        }else if(opt == 2) {
            for (int i = N-2; i >= 0; i--) {
                for (int j = 0; j < N; j++) {
                    if(board[i][j] == 0) {
                        continue;
                    }
                    int tmp = i+1;
                    while(tmp < N && board[tmp][j]==0){
                        tmp++;
                    }
                    if(tmp>=N){
                        board[N-1][j] = board[i][j];
                        board[i][j] = 0;
                        continue;
                    }
                    if(board[i][j] == board[tmp][j] && !visited[tmp][j]){
                        board[tmp][j] *= 2;
                        visited[tmp][j] = true;
                        board[i][j] = 0;
                    }else{
                        board[tmp-1][j] = board[i][j];
                        if(tmp-1 != i){
                            board[i][j] = 0;
                        }
                    }
                }
            }
        }else if(opt == 3) {
            for (int j = 1; j < N; j++) {
                for (int i = 0; i < N; i++) {
                    if(board[i][j] == 0) {
                        continue;
                    }
                    int tmp = j-1;
                    while(tmp >= 0 && board[i][tmp]==0){
                        tmp--;
                    }
                    if(tmp<0){
                        board[i][0] = board[i][j];
                        board[i][j] = 0;
                        continue;
                    }
                    if(board[i][j] == board[i][tmp] && !visited[i][tmp]){
                        board[i][tmp] *= 2;
                        visited[i][tmp] = true;
                        board[i][j] = 0;
                    }else{
                        board[i][tmp+1] = board[i][j];
                        if(tmp+1 != j){
                            board[i][j] = 0;
                        }
                    }
                }
            }
        }else if(opt == 4) {
            for (int j = N-2; j >= 0; j--) {
                for (int i = 0; i < N; i++) {
                    if(board[i][j] == 0) {
                        continue;
                    }
                    int tmp = j+1;
                    while(tmp < N && board[i][tmp]==0){
                        tmp++;
                    }
                    if(tmp>=N){
                        board[i][N-1] = board[i][j];
                        board[i][j] = 0;
                        continue;
                    }
                    if(board[i][j] == board[i][tmp] && !visited[i][tmp]){
                        board[i][tmp] *= 2;
                        visited[i][tmp] = true;
                        board[i][j] = 0;
                    }else{
                        board[i][tmp-1] = board[i][j];
                        if(tmp-1 != j){
                            board[i][j] = 0;
                        }
                    }
                }
            }
        }
    }
}
```
