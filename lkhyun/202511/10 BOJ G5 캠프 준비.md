```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringBuilder sb = new StringBuilder();
    static StringTokenizer st;
    static int N,L,R,X;
    static int[] problems;
    static int answer = 0;
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        L = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());
        X = Integer.parseInt(st.nextToken());

        problems = new int[N];
        st = new StringTokenizer(br.readLine());
        for(int i=0; i<N;i++){
            problems[i] = Integer.parseInt(st.nextToken());
        }

        select(0,0,Integer.MAX_VALUE,0,0);

        bw.write(answer+"");
        bw.close();
    }
    public static void select(int sum, int max, int min, int depth, int count){
        if(depth == N){
            if(L <= sum && sum <= R && (max-min) >= X && count >= 2) answer++;
            return;
        }
        int newMax = Math.max(max,problems[depth]);
        int newMin = Math.min(min,problems[depth]);
        select(sum+problems[depth], newMax, newMin, depth+1, count+1);

        select(sum, max, min, depth+1, count);
    }
}
```
