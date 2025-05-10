```java
import java.io.*;
import java.util.*;

public class Main {
    static int N;
    static long B;
    static int[][] matrix;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st;
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        B = Long.parseLong(st.nextToken());
        matrix = new int[N][N];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                matrix[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        int[][] result;
        result = pow(matrix, B);
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                bw.write(result[i][j] + " ");
            }
            bw.write("\n");
        }
        bw.close();
    }
    static public int[][] mul(int[][] a, int[][] b) {
        int[][] c = new int[N][N];
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                for (int k = 0; k < N; k++) {
                    c[i][j] = (c[i][j] + (a[i][k] * b[k][j]) % 1000) % 1000;
                }
            }
        }
        return c;
    }
    static public int[][] pow(int[][] a, long n) {
        if(n == 1){
            int[][] result = new int[N][N];
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < N; j++) {
                    result[i][j] = a[i][j] % 1000;
                }
            }
            return result;
        }
        if(n%2 == 0){
            return pow(mul(a,a),n/2);
        }else{
            return mul(pow(mul(a,a),n/2),a);
        }
    }
}

```
