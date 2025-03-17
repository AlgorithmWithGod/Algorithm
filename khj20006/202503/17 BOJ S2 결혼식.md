```

import java.util.*;
import java.io.*;

public class Main {

	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");
	
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Integer.parseInt(st.nextToken());
	}
	static long nextLong() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Long.parseLong(st.nextToken());
	}
	static void ioClose() throws Exception {bw.flush();bw.close();br.close();}
	
	/*
	 * [solving strategy]
	 * 친구들을 정점으로, 친구 관계를 간선으로 보고 인접 리스트 방식의 그래프 V를 생성합니다.
	 * 1의 친구들은 모두 V[1]에 들어있고, 그 친구들까지 V에서 찾아냅니다.
	 * 
	 * [description]
	 * - N, M : 정점, 간선의 개수
	 * - V : 인접 리스트
	 * 
	 * - ready() : input 처리 및 인접 리스트로 그래프 생성
	 * - solve() : 친구, 친구의 친구 탐색 -> 정답 출력
	 */
	
	static int N, M;
	static List<Integer>[] V;
	
	public static void main(String[] args) throws Exception {
		//--------------솔루션 코드를 작성하세요.--------------------------------
		
		ready();
		solve();
		
		ioClose();
		
	}
	
	static void ready() throws Exception {
		
		N = nextInt();
		M = nextInt();
		V = new List[N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		
		for(int i=1;i<=M;i++) {
			int a = nextInt(), b = nextInt();
			V[a].add(b);
			V[b].add(a);
		}
		
	}
	
	static void solve() throws Exception {
		
		boolean[] chk = new boolean[N+1];
		chk[1] = true;
		for(int i:V[1]) {
			chk[i] = true;
			for(int j:V[i]) chk[j] = true;
		}
		int cnt = 0;
		for(int i=2;i<=N;i++) cnt += chk[i] ? 1 : 0;
		bw.write(cnt + "\n");
		
	}

}


```
