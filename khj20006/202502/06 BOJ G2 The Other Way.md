```java

import java.util.*;
import java.io.*;

class Edge{
	int x;
	long c;
	Edge(int x, long c){
		this.x = x;
		this.c = c;
	}
}

class Element {
	long dist, cnt;
	int node;
	Element(long dist, long cnt, int node){
		this.dist = dist;
		this.cnt = cnt;
		this.node = node;
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
	static List<Edge>[] V;
	static long[] D;
	static long[] C;
	static int N, M, S, E;
	static long mod = (long)1e9 + 9, INF = 1234567890123456789L;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
		
		bwEnd();
	}
	
	static void ready() throws Exception{
		
		nextLine();
		N = nextInt();
		M = nextInt();
		S = nextInt();
		E = nextInt();
		V = new ArrayList[N+1];
		D = new long[N+1];
		
		Arrays.fill(D, INF);
		C = new long[N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		
		for(int i=0;i<M;i++) {
			nextLine();
			int a = nextInt(), b = nextInt();
			long c = nextLong();
			V[a].add(new Edge(b,c));
			V[b].add(new Edge(a,c));
		}
		
	}
	
	static void solve() throws Exception{

		dijkstra(S);
		bw.write(C[E]%mod + "\n");
		
	}
	
	static void dijkstra(int start) {
		
		D[start] = 0;
		C[start] = 1;
		PriorityQueue<Element> PQ = new PriorityQueue<>((a,b) -> {
			if(a.dist == b.dist) return 0;
			if(a.dist < b.dist) return -1;
			return 1;
		});
		PQ.offer(new Element(0,1,start));
		while(!PQ.isEmpty()) {
			Element now = PQ.poll();
			if(now.dist > D[now.node]) continue;
			for(Edge e : V[now.node]) {
				if(D[e.x] > now.dist + e.c) {
					D[e.x] = now.dist + e.c;
					C[e.x] = C[now.node]; 
					PQ.offer(new Element(D[e.x], C[e.x], e.x));
				}
				else if(D[e.x] == now.dist + e.c) {
					C[e.x] = (C[e.x] + C[now.node]) % mod; 
				}
			}
		}
		
	}
	
}

```
