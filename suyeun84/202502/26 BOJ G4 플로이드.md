```java
import java.util.*;
import java.io.*;

public class boj11404 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static void end() throws Exception {
		bw.flush();
		bw.close();
		br.close();
	}
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt(); //도시 개수
		nextLine();
		int M = nextInt(); //버스 개수
		int[][] answer = new int[N+1][N+1];
		for (int i = 1; i < N+1; i++) {
			Arrays.fill(answer[i], Integer.MAX_VALUE);
		}
		
		for (int i = 0; i < M; i++) {
			nextLine();
			int a = nextInt();
			int b = nextInt();
			int c = nextInt();
			answer[a][b] = Math.min(answer[a][b], c);
		}

		for (int k = 1; k < N+1; k++) {
			for (int i = 1; i < N+1; i++) {
				for (int j = 1; j < N+1; j++) {
					if (i == j) {
						answer[i][j] = 0;
						continue;
					}
					if (answer[i][k] == Integer.MAX_VALUE || answer[k][j] == Integer.MAX_VALUE) continue;
					answer[i][j] = Math.min(answer[i][j], answer[i][k]+answer[k][j]);
				}
			}
		}
		for (int i = 1; i < N+1; i++) {
			for (int j = 1; j < N+1; j++) {
				if (answer[i][j] == Integer.MAX_VALUE) {
					bw.write("0 ");
					continue;
				}
				bw.write(answer[i][j]+" ");
			}
			bw.write("\n");
			bw.flush();
		}
		end();
	}
	
	static class Node {
		int a;
		int b;
		int c;
		public Node(int a, int b, int c) {
			this.a = a;
			this.b = b;
			this.c = c;
		}
	}
}

```
