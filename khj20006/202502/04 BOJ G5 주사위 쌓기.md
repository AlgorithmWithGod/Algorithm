```java

import java.util.*;
import java.io.*;

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static long nextLong() {return Long.parseLong(st.nextToken());}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	public static void main(String[] args) throws Exception {

		int[][] ch = {
				{1,2,3,4},
				{0,2,4,5},
				{0,1,3,5},
				{0,2,4,5},
				{0,1,3,5},
				{1,2,3,4}
		};
		int[] op = {5,3,4,1,2,0};
		
		nextLine();
		int N = nextInt();
		int[][] Dices = new int[N][6];
		for(int i=0;i<N;i++) {
			nextLine();
			for(int j=0;j<6;j++) Dices[i][j] = nextInt();
		}
		
		int ans = 0;
		for(int t=0;t<6;t++) {
			int res = 0;
			for(int k=0;k<4;k++) res = Math.max(res, Dices[0][ch[t][k]]);
			
			int prev = Dices[0][t];
			for(int i=1;i<N;i++) {
				int down = 0;
				while(down < 6) {
					if(prev == Dices[i][down]) break;
					down++;
				}
				int up = op[down];
				int max = 0;
				for(int k=0;k<4;k++) max = Math.max(max, Dices[i][ch[up][k]]);
				res += max;
				prev = Dices[i][up];
			}
			ans = Math.max(ans, res);
		}
		
		bw.write(ans+"\n");
		
		bwEnd();
	}

}

```
