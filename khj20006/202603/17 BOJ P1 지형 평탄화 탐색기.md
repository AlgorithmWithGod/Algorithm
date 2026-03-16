```java
import java.io.*;
import java.util.*;

public class BOJ33908 {

    static class Count {
        int[] count;
        Count() {
            count = new int[1953125];
        }

        void add(int value) {
            if(value < 0) return;
            count[value]++;
        }

        void remove(int value) {
            if(value < 0) return;
            count[value]--;
        }

        int get(int value) {
            return count[value];
        }
    }

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static int N, M, Q;
    static int[][] arr;

    static Count[][] type;

    public static void main(String[] args) throws Exception {
        // 0. Input

        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        arr = new int[N][M];
        for(int i=0;i<N;i++) {
            st = new StringTokenizer(br.readLine());
            for(int j=0;j<M;j++) {
                arr[i][j] = Integer.parseInt(st.nextToken()) - 1;
            }
        }

        // 1. Find All Types

        type = new Count[10][];
        for(int r=1;r<=9;r++) {
            type[r] = new Count[9/r + 1];
        }

        for(int r=1;r<=9;r++) for(int c=1;r*c<=9;c++) {
            type[r][c] = new Count();
            for(int i=0;i+r<=N;i++) for(int j=0;j+c<=M;j++) {
                type[r][c].add(compute(i, j, r, c));
            }
        }

        // 2. Solve queries

        Q = Integer.parseInt(br.readLine());
        while(Q-- > 0) {
            st = new StringTokenizer(br.readLine());
            int q = Integer.parseInt(st.nextToken());
            if(q == 1) {
                int x = Integer.parseInt(st.nextToken()) - 1;
                int y = Integer.parseInt(st.nextToken()) - 1;
                int h = Integer.parseInt(st.nextToken()) - 1;
                for(int r=1;r<=9;r++) for(int c=1;r*c<=9;c++) {
                    for(int i=Math.max(x-r+1, 0);i<=Math.min(x, N-r);i++) for(int j=Math.max(y-c+1, 0);j<=Math.min(y, M-c);j++) {
                        type[r][c].remove(compute(i, j, r, c));
                    }
                }
                arr[x][y] = h;
                for(int r=1;r<=9;r++) for(int c=1;r*c<=9;c++) {
                    for(int i=Math.max(x-r+1, 0);i<=Math.min(x, N-r);i++) for(int j=Math.max(y-c+1, 0);j<=Math.min(y, M-c);j++) {
                        type[r][c].add(compute(i, j, r, c));
                    }
                }
            }
            else {
                int r = Integer.parseInt(st.nextToken());
                int c = Integer.parseInt(st.nextToken());
                int[][] arr2 = new int[r][c];
                int min = 4, max = -1;
                for(int i=0;i<r;i++) for(int j=0;j<c;j++) {
                    arr2[i][j] = Integer.parseInt(st.nextToken()) - 1;
                    min = Math.min(min, arr2[i][j]);
                    max = Math.max(max, arr2[i][j]);
                }

                int answer = 0;
                for(int z=-min;z<=4-max;z++) {
                    int k = 1, value = 0;
                    for(int i=0;i<r;i++) for(int j=0;j<c;j++) {
                        value += k * (arr2[i][j] + z);
                        k *= 5;
                    }
                    answer += type[r][c].get(value);
                }

                bw.write(answer + "\n");
            }
        }
        bw.close();
    }

    static int compute(int x, int y, int r, int c) {
        if(0 <= x && x+r <= N && 0 <= y && y+c <= M) {
            int k = 1, value = 0;
            for(int i=x;i<x+r;i++) for(int j=y;j<y+c;j++) {
                value += k * arr[i][j];
                k *= 5;
            }
            return value;
        }
        return -1;
    }

}
```
