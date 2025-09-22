```java
import java.io.*;
import java.util.*;

class IOController {
    BufferedReader br;
    BufferedWriter bw;
    StringTokenizer st;

    public IOController() {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer("");
    }

    String nextLine() throws Exception {
        String line = br.readLine();
        st = new StringTokenizer(line);
        return line;
    }

    String nextToken() throws Exception {
        while (!st.hasMoreTokens())
            nextLine();
        return st.nextToken();
    }

    int nextInt() throws Exception {
        return Integer.parseInt(nextToken());
    }

    long nextLong() throws Exception {
        return Long.parseLong(nextToken());
    }

    double nextDouble() throws Exception {
        return Double.parseDouble(nextToken());
    }

    void close() throws Exception {
        bw.flush();
        bw.close();
    }

    void write(String content) throws Exception {
        bw.write(content);
    }

}

public class Main {

    static IOController io;

    //

    static final int INF = (int)1e9 + 7;

    static final int[] dx = {1,0,-1,0};
    static final int[] dy = {0,1,0,-1};

    static int N, M, X, Y, A, B, C;
    static int[][] h;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        N = io.nextInt();
        M = io.nextInt();
        X = io.nextInt();
        Y = io.nextInt();
        A = io.nextInt();
        B = io.nextInt();
        C = io.nextInt();
        h = new int[N+1][M+1];
        int EX = -1, EY = -1, max = -1;
        for(int i=1;i<=N;i++) for(int j=1;j<=M;j++) {
            h[i][j] = io.nextInt();
            if(h[i][j] > max) {
                max = h[i][j];
                EX = i;
                EY = j;
            }
        }

        PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[0]-b[0]);
        pq.offer(new int[]{0,X,Y});
        int[][] dist = new int[N+1][M+1];
        for(int i=1;i<=N;i++) Arrays.fill(dist[i], INF);
        dist[X][Y] = 0;
        while(!pq.isEmpty()) {
            int[] cur = pq.poll();
            int d = cur[0], x = cur[1], y = cur[2];
            if(d > dist[x][y]) continue;
            if(x == EX && y == EY) {
                io.write(d + "\n");
                io.close();
                return;
            }
            for(int i=0;i<4;i++) {
                int xx = x + dx[i], yy = y + dy[i];
                if(xx<1 || xx>N || yy<1 || yy>M || Math.abs(h[xx][yy]-h[x][y]) > C) continue;
                int cost = d;
                if(h[xx][yy] > h[x][y]) cost += A*(h[xx][yy]-h[x][y]);
                if(h[xx][yy] < h[x][y]) cost += B*(h[x][y]-h[xx][yy]);
                if(h[xx][yy] == h[x][y]) cost++;
                if(dist[xx][yy] > cost) {
                    dist[xx][yy] = cost;
                    pq.offer(new int[]{cost,xx,yy});
                }
            }
        }
        io.write("-1");


        io.close();

    }

}
```
