```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static int[][] matrix;
    static List<int[]> shiftList;
    static List<int[]> cloudList;
    static int[] di = {0,0,-1,-1,-1,0,1,1,1};
    static int[] dj = {0,-1,-1,0,1,1,1,0,-1};

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        matrix = new int[N+1][N+1];
        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= N; j++) {
                matrix[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        shiftList = new ArrayList<>(M);
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            shiftList.add(new int[]{Integer.parseInt(st.nextToken()),Integer.parseInt(st.nextToken())});
        }

        cloudList = new ArrayList<>();
        cloudList.add(new int[]{N,1});
        cloudList.add(new int[]{N,2});
        cloudList.add(new int[]{N-1,1});
        cloudList.add(new int[]{N-1,2});

        for (int[] curShift : shiftList) {
            int cloudSize = cloudList.size();
            for (int i = 0; i < cloudSize; i++) {
                int[] cur = cloudList.get(i);
                shift(cur, curShift[0],curShift[1]);
                matrix[cur[0]][cur[1]]++;
            }

            for (int i = 0; i < cloudSize; i++) {
                int[] cur = cloudList.get(i);
                for (int j = 2; j <= 8; j+=2) {
                    int ni = cur[0] + di[j];
                    int nj = cur[1] + dj[j];
                    if(ni>=1 && ni<=N && nj>=1 && nj<=N && matrix[ni][nj]>0){
                        matrix[cur[0]][cur[1]]++;
                    }
                }
            }

            boolean[][] visited = new boolean[N+1][N+1];
            for (int[] cur : cloudList) {
                visited[cur[0]][cur[1]] = true;
            }
            cloudList.clear();
            
            for (int i = 1; i <= N; i++) {
                for (int j = 1; j <= N; j++) {
                    if(!visited[i][j] && matrix[i][j]>=2){
                        cloudList.add(new int[]{i,j});
                        matrix[i][j] -= 2;
                    }
                }
            }
        }
        
        int ans = 0;
        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= N; j++) {
                ans += matrix[i][j];
            }
        }
        bw.write(ans+"");
        bw.close();
    }
    static void shift(int[] cur, int direction, int count){
        cur[0] += di[direction]*count;
        cur[1] += dj[direction]*count;

        cur[0] = (((cur[0] - 1) % N) + N) % N + 1;
        cur[1] = (((cur[1] - 1) % N) + N) % N + 1;
    }
}
```
