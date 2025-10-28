```java
import java.util.*;
import java.io.*;

public class Main{
    static class State{
        int x,y;
        int[] row = new int[3];
        int[] col = new int[3];
        State(int x, int y){
            this.x = x;
            this.y = y;
        }
        public void rolling(int direction, int[][] map) throws Exception{
            if(direction == 1){ //동쪽
                if(y == map[0].length-1) return;
                int temp = col[2];
                col[2] = row[2];
                row[2] = row[1];
                row[1] = row[0];
                row[0] = temp;
                y++;
                check();
                return;
            }
            if(direction == 2){ //서쪽
                if(y == 0) return;
                int temp = col[2];
                col[2] = row[0];
                row[0] = row[1];
                row[1] = row[2];
                row[2] = temp;
                y--;
                check();
                return;
            }
            if(direction == 3){ //북쪽
                if(x == 0) return;
                int temp = col[2];
                col[2] = col[0];
                col[0] = row[1];
                row[1] = col[1];
                col[1] = temp;
                x--;
                check();
                return;
            }
            if(direction == 4){ //남쪽
                if(x == map.length-1) return;
                int temp = col[2];
                col[2] = col[1];
                col[1] = row[1];
                row[1] = col[0];
                col[0] = temp;
                x++;
                check();
                return;
            }
        }
        public void check() throws Exception{
            if(map[x][y] == 0){
                    map[x][y] = col[2];
                }else{
                    col[2] = map[x][y];
                    map[x][y] = 0;
                }
                bw.write(row[1]+"\n");
        }
    }
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringBuilder sb = new StringBuilder();
    static StringTokenizer st;
    static int N,M,X,Y,K;
    static int[][] map;
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        X = Integer.parseInt(st.nextToken());
        Y = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        map = new int[N][M];
        for(int i = 0; i<N; i++){
            st = new StringTokenizer(br.readLine());
            for(int j = 0; j<M; j++){
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        State dice = new State(X,Y);
        
        st = new StringTokenizer(br.readLine());
        for(int i = 0; i<K; i++){
            int cmd = Integer.parseInt(st.nextToken());
            dice.rolling(cmd, map);
        }
        bw.close();
    }
}
```
