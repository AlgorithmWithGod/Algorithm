```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] original;
    static long[] leftSum;
    static long[] rightSum;
    static long total;

    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        
        original = new int[N];
        leftSum = new long[N];
        rightSum = new long[N];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            original[i] = Integer.parseInt(st.nextToken());            
        }
        
        // 왼쪽에서 오른쪽으로
        leftSum[0] = original[0];
        for (int i = 1; i < N; i++) {
            leftSum[i] = leftSum[i-1] + original[i];
        }
        
        // 오른쪽에서 왼쪽으로
        rightSum[N-1] = original[N-1];
        for (int i = N-2; i >= 0; i--) {
            rightSum[i] = rightSum[i+1] + original[i];
        }
        
        total = leftSum[N-1];
        long max = 0;
        
        //벌통이 맨 오른쪽, 벌1이 맨 왼쪽 고정, 벌2 위치 선택
        for (int i = 1; i < N-1; i++) {
            long bee1 = total - original[0] - original[i];
            long bee2 = total - leftSum[i];
            max = Math.max(max, bee1 + bee2);
        }
        
        //벌통이 맨 왼쪽, 벌1이 맨 오른쪽 고정, 벌2 위치 선택  
        for (int i = N-2; i > 0; i--) {
            long bee1 = total - original[N-1] - original[i];
            long bee2 = total - rightSum[i];
            max = Math.max(max, bee1 + bee2);
        }
        
        //벌1이 맨 왼쪽, 벌2가 맨 오른쪽 고정, 벌통 위치 선택
        for (int i = 1; i < N-1; i++) {
            long bee1 = leftSum[i] - original[0];
            long bee2 = rightSum[i] - original[N-1];
            max = Math.max(max, bee1 + bee2);
        }
        
        bw.write(max + "");
        bw.close();
    }
}
```
