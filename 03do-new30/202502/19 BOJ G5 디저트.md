```java
import java.util.*;
import java.io.*;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

		StringTokenizer st = new StringTokenizer(br.readLine());
		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());

		// point[i][j] = i번째 디저트를 j일째에 먹는 경우 만족감
		int[][] point = new int[M + 1][N + 1];
		for (int i = 1; i < M + 1; i++) {
			st = new StringTokenizer(br.readLine());
			for (int j = 1; j < N + 1; j++) {
				point[i][j] = Integer.parseInt(st.nextToken());
			}
		}
		
		// 한 주기마다 얻을 수 있는 만족감의 최댓값을 출력한다.

		// dp[day][dessert] = dessert를 day일에 먹는 경우 얻을 수 있는 만족감의 최대
		int[][] dp = new int[N + 1][M + 1];
		
		for (int day = 1; day < N + 1; day++) {
			for (int dessert = 1; dessert < M + 1; dessert++) {
				if (day == 1) {
					dp[day][dessert] = point[dessert][day];
					continue;
				}
				for (int prev = 1; prev < M + 1; prev++) {
					if (prev == dessert) { 
						// 전날에 같은 디저트를 먹은 경우
						dp[day][dessert] = Integer.max(dp[day][dessert], 
								dp[day-1][dessert] + point[dessert][day]/2); // 만족감이 감소한다.
					} else {
						// 전날에 다른 디저트를 먹은 경우
						dp[day][dessert] = Integer.max(dp[day][dessert],
								dp[day-1][prev] + point[dessert][day]); // 만족감이 감소하지 않는다.
					}
					
				}
			}
		}

		int answer = 0;
		for (int dessert = 1; dessert < M+1; dessert++) {
			answer = Integer.max(answer, dp[N][dessert]);
		}
		System.out.println(answer);

		br.close();
	}
}

```
