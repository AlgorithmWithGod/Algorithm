```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringBuilder sb = new StringBuilder();
    static StringTokenizer st;
    static int N;
    static int[] helowrd = new int[7];
    static boolean[] numbers = new boolean[10];
    static boolean finished;
    static int A,B;
    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        backtracking(0);
        if(A == 0){
            bw.write("No Answer");
            bw.close();
            return;
        }
        bw.write(String.format("%7d\n", A));
        bw.write(String.format("+ %5d\n", B));
        bw.write("-------\n");
        bw.write(String.format("%7d", N));
        bw.close();
    }
    public static void backtracking(int depth){
        if(finished) return;
        if(depth == 7){
            int a = 10000*helowrd[0] + 1000*helowrd[1] + 100*helowrd[2] + 10*helowrd[2] + helowrd[3];
            int b = 10000*helowrd[4] + 1000*helowrd[3] + 100*helowrd[5] + 10*helowrd[2] + helowrd[6];
            if((a+b) == N){
                finished = true;
                A = a;
                B = b;
            }
            return;
        }

        for(int i = 0; i<10; i++){
            if(depth==0 && i==0) continue;
            if(depth==4 && i==0) continue;
            if(!numbers[i]){
                helowrd[depth] = i;
                numbers[i] = true;
                backtracking(depth+1);
                numbers[i] = false;
            }
        }
    }
}
```
