```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	private static final int N = 11;
	private static int[][] Scores = new int[N][N];
	private static boolean[] Used = new boolean[N];
	private static int MaxSum = 0;

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int t = Integer.parseInt(br.readLine());
		while(t-->0){
			for (int i = 0; i < N; i++) {
				StringTokenizer st = new StringTokenizer(br.readLine());
				for (int j = 0; j < N; j++) {
					Scores[i][j] = Integer.parseInt(st.nextToken());
				}
			}
			Used = new boolean[N];
			MaxSum = 0;
			dfs(0, 0);
			System.out.println(MaxSum);
		}
	}

	private static void dfs(int pos, int currentSum) {
		if (pos == N) {
			if (currentSum > MaxSum) {
				MaxSum = currentSum;
			}
			return;
		}
		for (int player = 0; player < N; player++) {
			if(Scores[player][pos] == 0) continue;
			if (!Used[player]) {
				Used[player] = true;
				dfs(pos + 1, currentSum + Scores[player][pos]);
				Used[player] = false;
			}
		}
	}
}

```
