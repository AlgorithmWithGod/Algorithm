```java
import java.io.*;
import java.util.*;

public class Main {
	
	private static int N;
	private static int[][] S;
	
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		
		N = Integer.parseInt(br.readLine());
		S = new int[N][N];
		for (int i =0; i < N; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			for (int j = 0; j < N; j++) {
				S[i][j] = Integer.parseInt(st.nextToken());
			}
		}
		
		boolean[] teamOne = new boolean[N];
		int answer = solve(0, teamOne);
		bw.write(answer + "\n");
		
		br.close();
		bw.flush();
		bw.close();
	}

	private static int solve(int idx, boolean[] teamOne) {
		if (idx == N) {
			int scoreOne = 0;
			int scoreTwo = 0;
			for (int i = 0; i < N; i++) {
				for (int j = 0; j < N; j++) {
					if (teamOne[i] != teamOne[j]) { continue; }
					if (teamOne[i]) {
						scoreOne += S[i][j];
					} else {
						scoreTwo += S[i][j];
					}
				}
			}
			return Math.abs(scoreOne - scoreTwo);
		}
		
		// idx가 팀1에 속하는 경우
		teamOne[idx] = true;
		int result1 = solve(idx + 1, teamOne);
		// idx가 팀2에 속하는 경우
		teamOne[idx] = false;
		int result2 = solve(idx + 1, teamOne);
		return Integer.min(result1, result2);
	}
}

```
