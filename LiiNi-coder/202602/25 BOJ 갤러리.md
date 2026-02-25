```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		int M = Integer.parseInt(st.nextToken());
		int N = Integer.parseInt(st.nextToken());
		char[][] map = new char[M][N];
		for (int i = 0; i < M; i++) {
			map[i] = br.readLine().toCharArray();
		}
		int answer = 0;

		for(int i = 0; i < M - 1; i++) {
			for(int j = 1; j < N - 1; j++) {
				if(map[i][j] == 'X' && map[i][j+1] == 'X' &&
					map[i+1][j] == '.' && map[i+1][j+1] == '.') {
					answer++;
					j++; // 건너뛰ㅏ어야함
				}
			}

			for(int j = 1; j < N - 1; j++) {
				if(map[i][j] == '.' && map[i][j+1] == '.' &&
					map[i+1][j] == 'X' && map[i+1][j+1] == 'X') {
					answer++;
					j++;
				}
			}
		}

		for(int j = 0; j < N - 1; j++) {
			for(int i = 1; i < M - 1; i++) {

				if(map[i][j] == 'X' && map[i+1][j] == 'X' &&
					map[i][j+1] == '.' && map[i+1][j+1] == '.') {
					answer++;
					i++;
				}
			}

			for(int i = 1; i < M - 1; i++) {
				if(map[i][j] == '.' && map[i+1][j] == '.' &&
					map[i][j+1] == 'X' && map[i+1][j+1] == 'X') {
					answer++;
					i++;
				}
			}
		}
		System.out.println(answer);
	}
}


```
