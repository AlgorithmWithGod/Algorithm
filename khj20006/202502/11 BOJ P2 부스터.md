```java

import java.util.*;
import java.io.*;

class Point{
	int x, y, id;
	Point(int x, int y, int id){
		this.x = x;
		this.y = y;
		this.id = id;
	}
}

class Query{
	int a, b, v, id;
	Query(int a, int b, int v, int id){
		this.a = a;
		this.b = b;
		this.v = v;
		this.id = id;
	}
}

class Edge{
	int a, b, c;
	Edge(int a, int b, int c){
		this.a = a;
		this.b = b;
		this.c = c;
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
	static Point[] arr;
	static Query[] que;
	static int[] root;
	static int N, Q;
	static List<Edge> edges;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		nextLine();
		N = nextInt();
		Q = nextInt();
		root = new int[N];
		arr = new Point[N];
		for(int i=0;i<N;i++) {
			root[i] = i;
			nextLine();
			int x = nextInt(), y = nextInt();
			arr[i] = new Point(x,y,i);
		}
		
		que = new Query[Q];
		for(int i=0;i<Q;i++) {
			nextLine();
			int a = nextInt(), b = nextInt(), v = nextInt();
			que[i] = new Query(a-1,b-1,v,i);
		}
		edges = new ArrayList<>();
		
	}
	
	static void solve() throws Exception{

		Arrays.sort(arr, (a,b) -> a.x-b.x);
		for(int i=1;i<N;i++) {
			 edges.add(new Edge(arr[i-1].id, arr[i].id, arr[i].x - arr[i-1].x));
		}
		Arrays.sort(arr, (a,b) -> a.y-b.y);
		for(int i=1;i<N;i++) {
			edges.add(new Edge(arr[i-1].id, arr[i].id, arr[i].y - arr[i-1].y));
		}
		Collections.sort(edges, (a,b) -> a.c-b.c);
		
		Arrays.sort(que, (a,b) -> a.v-b.v);
		boolean[] ans = new boolean[Q];
		int idx = 0;
		for(int i=0;i<Q;i++) {
			while(idx<edges.size() && edges.get(idx).c <= que[i].v) {
				int x = f(edges.get(idx).a), y = f(edges.get(idx).b);
				if(x != y) root[x] = y;
				idx++;
			}
			int x = f(que[i].a), y = f(que[i].b);
			ans[que[i].id] = x == y; 
		}
		
		for(int i=0;i<Q;i++) bw.write(ans[i] ? "YES\n" : "NO\n");
		
	}
	
	static int f(int x) { return x==root[x] ? x : (root[x]=f(root[x]));}
	
	
}

```
