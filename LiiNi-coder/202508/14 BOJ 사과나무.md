```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Main {
	private static BufferedReader br;
	private static int N;
	private static int[][] Map;
	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		Map = new int[N+1][N+1];
		for(int r = 1; r < N+1; r++){
			String[] temp = br.readLine().split(" ");
			for(int c = 1; c<N+1; c++){
				Map[r][c] = Integer.parseInt(temp[c-1]);
			}
		}

		int answer = Integer.MIN_VALUE;
		//누적합 구하기
		var preMap = new int[N+1][N+1];
		for(int r = 1; r < N+1; r++){
			for(int c = 1; c < N+1; c++){
				preMap[r][c] = Map[r][c] + preMap[r-1][c] + preMap[r][c-1] - preMap[r-1][c-1];
			}
		}

		// for(int[] line: preMap){
		// 	System.out.println(Arrays.toString(line));
		// }


		for(int r = 1; r<N+1; r++){
			for(int c = 1; c<N+1; c++){
				for(int n = 0; n<N+1; n++){
					int[] rightDown = new int[2];
					rightDown[0] = r+n;
					rightDown[1] = c+n;
					if(rightDown[0] >= N+1 || rightDown[1] >= N+1){
						continue;
					}

					int partitialSum;
					if(n == 0){
						partitialSum = Map[r][c];
					}else{
						partitialSum=
						preMap[rightDown[0]][rightDown[1]]
						- preMap[rightDown[0] - (n+1)][rightDown[1]]
						- preMap[rightDown[0]][rightDown[1] - (n+1)]
						+ preMap[r-1][c-1];
					}
					answer = Math.max(answer, partitialSum);
					//System.out.println(String.format("(r, c)=(%d, %d) (rd0, rd1)=(%d, %d), partitialSum: %d", r, c, rightDown[0], rightDown[1], partitialSum));
				}
			}
		}
		System.out.println(answer);
	}
}
```
