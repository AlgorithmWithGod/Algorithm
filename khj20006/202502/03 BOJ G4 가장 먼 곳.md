```java

import java.util.*;
import java.io.*;

class Node{
	int d, n;
	Node(int d, int n){
		this.d = d;
		this.n = n;
	}
}

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
	static int N;
	static int INF = 1234567890;
	static ArrayList<int[]>[] V;
	
	static int[] dijk(int s) {
		int[] D = new int[N+1];
		Arrays.fill(D, INF);
		D[s] = 0;
		PriorityQueue<Node> PQ = new PriorityQueue<>((a,b) -> a.d - b.d);
		PQ.offer(new Node(0,s));
		while(!PQ.isEmpty()) {
			Node now = PQ.poll();
			if(now.d > D[now.n]) continue;
			for(int[] next : V[now.n]) {
				if(D[next[0]] > now.d + next[1]) {
					D[next[0]] = now.d + next[1];
					PQ.offer(new Node(now.d+next[1],next[0]));
				}
			}
		}
		return D;
	}

	public static void main(String[] args) throws Exception {

		nextLine();
		N = nextInt();
		V = new ArrayList[N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		nextLine();
		int A = nextInt(), B = nextInt(), C = nextInt();
		nextLine();
		int M = nextInt();
		for(int i=0;i<M;i++) {
			nextLine();
			int a = nextInt(), b = nextInt(), c = nextInt();
			V[a].add(new int[] {b,c});
			V[b].add(new int[] {a,c});
		}
		int[] DA = dijk(A);
		int[] DB = dijk(B);
		int[] DC = dijk(C);
		
		int ans = 0, res = 0;
		for(int i=1;i<=N;i++) {
			int min = Math.min(DA[i], Math.min(DB[i], DC[i]));
			if(min > ans) {
				ans = min;
				res = i;
			}
		}
		bw.write(res+"\n");
		
		bwEnd();
	}

}

```
