```java
import java.awt.Point;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {

    static long ans;
    static int size;
    static long[][] arr,sumArr;
    static int[] dy = {0,1};
    static int[] dx = {1,0};

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        size = Integer.parseInt(br.readLine());
        ans = Integer.MIN_VALUE;

        arr = new long[size][size];
        sumArr = new long[size][size]; // i,j -> 0,0부터 i.j까지 직사각형 하
        for (int i = 0; i < size; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < size; j++) {
                arr[i][j] = Long.parseLong(st.nextToken());
            }
        }
    }

    private static void process() throws IOException {
        makeSumArr();

        for (int i = 0; i < size; i++) {
            for (int j = 0; j < size; j++) {
                calculate(i,j);
            }
        }

    }

    private static void calculate(int y, int x) {
        for (int i = 0; i < size; i++) {
            if ( y - i < 0 || x - i < 0) continue;
            long cur = sumArr[y][x];
            if ( y- i > 0) cur -= sumArr[y-i-1][x];
            if ( x - i > 0 ) cur -= sumArr[y][x-i-1];
            if ( x-i > 0 && y-i > 0) cur += sumArr[y-i-1][x-i-1];

            ans = Math.max(ans, cur);
        }

    }

    private static void makeSumArr() {

        for (int i = 0; i < size; i++) {
            for (int j = 0; j < size; j++) {
                if (i == 0 && j == 0) sumArr[i][j] =  arr[i][j];
                else if (i == 0) sumArr[i][j]=  sumArr[i][j-1] + arr[i][j];
                else if (j == 0) sumArr[i][j]  =  sumArr[i-1][j] + arr[i][j];
                else sumArr[i][j] = sumArr[i-1][j] + sumArr[i][j-1] + arr[i][j] - sumArr[i-1][j-1];

            }
        }


    }


    private static void print() {
        System.out.println(ans);
    }
}


```