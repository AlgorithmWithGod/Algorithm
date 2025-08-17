```java
import java.io.*;
import java.util.*;

public class Main {

    static int height,width;
    static int[][] arr;
    static int[][] dp;
    static int[] dy = {-1,0,1,0};
    static int[] dx = {0,1,0,-1};


    public static void main(String[] args) throws Exception {
        init();
        process();
        print();

    }

    public static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        height = Integer.parseInt(st.nextToken());
        width = Integer.parseInt(st.nextToken());
        arr = new int[height][width];
        dp = new int[height][width];

        for (int i = 0; i < height; i++) {
            Arrays.fill(dp[i],-1);
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < width; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }


    }

    public static void process(){
        dfs(0,0);
    }

    public static void print(){

        System.out.println(dp[0][0]);
    }

    public static int dfs(int y, int x){
        if ( y == height - 1 && x == width - 1 ) {
            return 1;
        }


        if(dp[y][x] != -1) return dp[y][x];

        dp[y][x] = 0;

        for (int i = 0; i < 4; i++){
            int ny = y + dy[i];
            int nx = x + dx[i];
            if (ny < 0 || ny >= height || nx < 0 || nx >= width) continue;
            if (arr[ny][nx] >= arr[y][x]) continue;

            dp[y][x] += dfs(ny, nx);
        }

        return dp[y][x];

    }

}


```