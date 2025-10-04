```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static int N;
    static int[] input;
    static int[] target;
    static int cnt1 = 0;
    static int cnt2 = 0;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        input = new int[N];
        target = new int[N];

        String temp1 = br.readLine();
        String temp2 = br.readLine();
        
        for(int i = 0;i<N;i++){
            input[i] = Character.getNumericValue(temp1.charAt(i));
            target[i] = Character.getNumericValue(temp2.charAt(i));
        }
        int[] input1 = input.clone();
        int[] input2 = input.clone();

        for(int i = 1; i<N; i++){
            if(input1[i-1] != target[i-1]){
                input1[i-1] ^= 1;
                input1[i] ^= 1;
                if(i+1 < N) {
                    input1[i + 1] ^= 1;
                }
                cnt1++;
            }
        }
        for (int i = 0; i < N; i++) {
            if(input1[i] != target[i]){
                cnt1 = Integer.MAX_VALUE;
                break;
            }
        }

        input2[0] ^= 1;
        input2[1] ^= 1;
        cnt2++;
        for (int i = 1; i < N; i++) {
            if(input2[i-1] != target[i-1]){
                input2[i-1] ^= 1;
                input2[i] ^= 1;
                if(i+1 < N) {
                    input2[i + 1] ^= 1;
                }
                cnt2++;
            }
        }
        for (int i = 0; i < N; i++) {
            if(input2[i] != target[i]){
                cnt2 = Integer.MAX_VALUE;
                break;
            }
        }
        int cnt = Math.min(cnt1, cnt2);
        if(cnt == Integer.MAX_VALUE){
            cnt = -1;
        }
        bw.write(cnt+"");
        bw.close();
    }
}
```
