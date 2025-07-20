```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] minimumCond = new int[4];
    static int[][] food;
    static int[] cost;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < 4; i++) {
            minimumCond[i] = Integer.parseInt(st.nextToken());
        }

        food = new int[N][5];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            food[i][0] = Integer.parseInt(st.nextToken()); //단백질
            food[i][1] = Integer.parseInt(st.nextToken()); //지방
            food[i][2] = Integer.parseInt(st.nextToken()); //탄수화물
            food[i][3] = Integer.parseInt(st.nextToken()); //비타민
            food[i][4] = Integer.parseInt(st.nextToken()); //가격
        }
        int ans = Integer.MAX_VALUE;
        String state = "";
        cost = new int[1<<N];
        loop:for (int i = 1; i < (1<<N); i++) {
            int[] sum = new int[5];
            for (int j = 0; j < N; j++) {
                if((i & (1<<j)) != 0){
                    for (int k = 0; k < 5; k++) {
                        sum[k] += food[j][k];
                    }
                }
            }
            for (int k = 0; k < 4; k++) {
                if(sum[k] < minimumCond[k]) continue loop;
            }
            if(ans > sum[4]){
                ans = sum[4];
                state = stateToStr(i);

            }else if(ans == sum[4]){
                String temp = stateToStr(i);
                if(state.compareTo(temp) > 0){
                    state = temp;
                }
            }

        }
        if(ans == Integer.MAX_VALUE){
            bw.write("-1\n");
        }else{
            bw.write(ans+"\n"+state);
        }
        bw.close();
    }
    static String stateToStr(int state){
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < N; i++) {
            if((state & (1<<i)) != 0){
                sb.append(i+1).append(" ");
            }
        }
        return sb.toString();
    }
}
```
