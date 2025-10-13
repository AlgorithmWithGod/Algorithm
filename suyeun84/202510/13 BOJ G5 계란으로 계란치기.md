```java
import java.io.*;
import java.util.*;

public class boj16987 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }
    
    static int N, answer = 0;
	public static void main(String[] args) throws Exception {
		nextLine();
		N = nextInt();
		Egg[] eggs = new Egg[N];
		for (int i = 0; i < N; i++) {
			nextLine();
			eggs[i] = new Egg(nextInt(), nextInt());
		}
		
		dfs(0, eggs);
		System.out.println(answer);
	}
	
	public static void dfs(int idx, Egg[] eggs) {
		if (idx == N) {
			int cnt = 0;
			for (int i = 0; i < N; i++) {
				if (eggs[i].s <= 0) cnt++;
			}
			answer = Math.max(answer, cnt);
			return;
		}
		if (eggs[idx].s < 0) dfs(idx+1, eggs);
		else {
			boolean flag = true;
			for (int i = 0; i < N; i++) {
				if (eggs[i].s <= 0 || idx == i) continue;
				flag = false;
				eggs[i].s -= eggs[idx].w;
				eggs[idx].s -= eggs[i].w;
				dfs(idx+1, eggs);
				eggs[i].s += eggs[idx].w;
				eggs[idx].s += eggs[i].w;
			}
			if (flag) dfs(idx+1, eggs);
		}
	}
	
	static class Egg {
		int s, w;
		public Egg(int s, int w) {
			this.s = s;
			this.w = w;
		}
	}
}

```
