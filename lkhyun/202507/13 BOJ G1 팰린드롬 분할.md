```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static boolean[][] dp;
    static int[] dp2;

    public static void main(String[] args) throws Exception{
        String str = br.readLine();
        int len = str.length();
        dp = new boolean[len][len];

        for (int i = 0; i < len; i++) { // 한 자리
            dp[i][i] = true;
        }
        for (int i = 0; i < len-1; i++) { // 두 자리
            if(str.charAt(i) == str.charAt(i+1)) {
                dp[i][i+1] = true;
            }
        }

        for (int i = 2; i < len; i++) { // 그외
            for (int j = 0; j+i < len; j++) {
                if(str.charAt(j) == str.charAt(i+j)){
                    dp[j][i+j] = dp[j+1][i+j-1];
                }else{
                    dp[j][i+j] = false;
                }
            }
        }

        dp2 = new int[len+1]; //0부터 시작해서 i까지의 문자까지 보았을 때 팰린드롬으로 분할하는 최소 개수
        Arrays.fill(dp2, Integer.MAX_VALUE);
        dp2[0] = 0; 

        for (int i = 1; i <= len; i++) { //모든 길이에 대해서
            for (int j = 0; j < i; j++) { //첫번째 문자부터 보기
                if(dp[j][i-1]){ //j지점에서 문자열 끝까지 팰린드롬이면
                    dp2[i] = Math.min(dp2[i], dp2[j] + 1); //j지점까지의 분할 개수와 j지점 이후는 팰린드롬이므로 1을 더해주기
                }
            }
        }

        bw.write(dp2[len] + "");
        bw.close();
    }
}
```
