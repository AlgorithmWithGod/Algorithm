```java
import java.io.*;
import java.util.*;

public class Main {
	public static void main(String[] args)throws IOException{
		BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
		List<int[]> arrs = new ArrayList<>();
		String line;
		while(true){
			line = br.readLine();
			if("".equals(line) || line == null){
				break;
			}
			StringTokenizer st=new StringTokenizer(line);
			int w=Integer.parseInt(st.nextToken());
			int b=Integer.parseInt(st.nextToken());
			arrs.add(new int[]{w,b});
		}

		int n = arrs.size();
		// dp[i][j][k] = i번째 멤버까지 보았을때, 백을 j명 뽑았고, 흑을 k명 뽑았을때의 최대 점수 합
		int[][][] dp = new int[n+1][16][16];
		for(int i=1; i<=n; i++){
			int w = arrs.get(i-1)[0];
			int b = arrs.get(i-1)[1];
			for(int j=0; j<=15; j++){
				for(int k=0; k<=15; k++){
					dp[i][j][k] = dp[i-1][j][k];
					if(j > 0)
						dp[i][j][k] = Math.max(dp[i][j][k], dp[i-1][j-1][k] + w);
					if(k > 0)
						dp[i][j][k]= Math.max(dp[i][j][k], dp[i-1][j][k-1] + b);
				}
			}
      //System.out.println(dp[i][w][b]);
		}
		System.out.println(dp[n][15][15]);
	}
}

```
