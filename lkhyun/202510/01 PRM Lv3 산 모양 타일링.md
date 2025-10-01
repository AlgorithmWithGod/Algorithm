```java
class Solution {
    public int solution(int n, int[] tops) {
        int answer = 0;
        int[][] dp = new int[(n*2)+1][2]; //dp[i][j] = i번째 위치까지 j의 형태로 둔 경우의 수
        //0이면 이후 타일에 영향없음
        //1이면 이후 타일에 영향
        dp[0][0] = 1;
        dp[0][1] = 1;
        for(int i=1;i<n*2;i++){
            if(i%2==0){ //삼각형
                dp[i][0] = (dp[i-1][1] + dp[i-1][0])%10007;
                dp[i][1] = dp[i-1][0];
            }else{ //역삼각형
                if(tops[i/2] == 1){
                    dp[i][0] = (dp[i-1][1] + dp[i-1][0]*2)%10007;
                }else{
                    dp[i][0] = (dp[i-1][1] + dp[i-1][0])%10007;
                }
                dp[i][1] = dp[i-1][0];
            }
        }
        return (dp[(n*2)-1][0] + dp[(n*2)-1][1]) % 10007;
    }
}
```
