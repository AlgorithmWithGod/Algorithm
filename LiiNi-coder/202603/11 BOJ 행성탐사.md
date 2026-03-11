```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main{
	public static void main(String[] args)throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());
		int K = Integer.parseInt(br.readLine());
		int[][] J = new int[N+1][M+1];
		int[][] O = new int[N+1][M+1];
		int[][] I = new int[N+1][M+1];

		
		for(int r = 1; r<=N; r++){
			String line = br.readLine();
			for(int c = 1 ; c<=M; c++){
				char ch = line.charAt(c-1);
				
				J[r][c] = J[r-1][c] + J[r][c-1] - J[r-1][c-1];
				O[r][c] = O[r-1][c] + O[r][c-1] - O[r-1][c-1];
				I[r][c] = I[r-1][c] + I[r][c-1] - I[r-1][c-1];
				if(ch == 'J')
					J[r][c]++;
				else if(ch == 'O')
					O[r][c]++;
				else
					I[r][c]++;
			}
		}

		StringBuilder sb = new StringBuilder();
		for(int i=0; i<K; i++){
			st = new StringTokenizer(br.readLine());
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			int c = Integer.parseInt(st.nextToken());
			int d = Integer.parseInt(st.nextToken());
			int j = J[c][d] - J[a-1][d] - J[c][b-1] + J[a-1][b-1];
			int o = O[c][d] - O[a-1][d] - O[c][b-1] + O[a-1][b-1];
			int ii = I[c][d] - I[a-1][d] - I[c][b-1] + I[a-1][b-1];

			sb.append(j).append(" ").append(o).append(" ").append(ii).append("\n");
		}

		System.out.print(sb);
	}
}
```
