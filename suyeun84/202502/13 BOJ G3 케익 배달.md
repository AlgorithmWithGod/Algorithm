```java
import java.util.*;
import java.io.*;

class Solution
{
	public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int N = Integer.parseInt(st.nextToken());
        ArrayList<Position> target = new ArrayList<>();
        long[][] dp = new long[N+1][5]; // 0:정위치 1:북 2:동 3:남 4:서
        int[][] dir = new int[][] {{0,0}, {-1,0}, {0,1}, {1,0}, {0,-1}};
        long answer = Long.MAX_VALUE;
        
        for (int i = 0; i< N+1; i++) {
        	st = new StringTokenizer(br.readLine());
        	target.add(new Position(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken())));
        	Arrays.fill(dp[i], Long.MAX_VALUE);
        }
        for (int i = 0 ; i < 5; i++) {
        	if (i == 0) {
        		dp[0][0] = 0;
        	} else {
        		dp[0][i] = 1;
        	}
        }

        for (int i = 1; i < N+1; i++) {
        	for (int j = 0; j < 5; j++) {
        		//이전꺼 위치
        		int y = target.get(i-1).y + dir[j][0];
        		int x = target.get(i-1).x + dir[j][1];
        		for (int z = 0; z < 5; z++) {
        			//이번꺼 위치
        			int ty = target.get(i).y + dir[z][0];
            		int tx = target.get(i).x + dir[z][1];
        			//목표 위치의 상하좌우
        			dp[i][z] = Math.min(dp[i][z], Math.abs(y-ty)+Math.abs(x-tx)+dp[i-1][j]);
        		}
        	}
        }
        for (int i = 0; i < 5; i++) {
        	answer = Math.min(answer, dp[N][i]);
        }
        System.out.println(answer);
	}
	
	static class Position {
		int y;
		int x;
		public Position(int y, int x) {
			this.y = y;
			this.x = x;
		}
	}
}

```
