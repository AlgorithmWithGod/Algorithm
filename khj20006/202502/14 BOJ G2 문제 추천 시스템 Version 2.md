### [C++]
```cpp

#include <iostream>
#include <set>
#include <tuple>
#include <bitset>
#include <functional>
using namespace std;
// 난이도, 번호, 종류, id
using problem = tuple<int, int, int, int>;

int main() {
	cin.tie(0)->sync_with_stdio(0);

	int N;
	cin >> N;
	set<problem> Total, Type[101]{}, Rank[101]{};

	bitset<200001> solved;

	int id = 0, numToId[200001]{};

	for (int i = 0, p, l, g; i < N; i++) {
		cin >> p >> l >> g;
		problem pr = { l,p,g,numToId[p]=id++ };
		Total.insert(pr);
		Type[g].insert(pr);
		Rank[l].insert(pr);
	}

	function isSolved = [&](problem pr) -> bool {return solved[get<3>(pr)]; };

	int M;
	for (cin >> M; M--;) {
		string op;
		cin >> op;
		if (op == "recommend") {
			int g, x;
			cin >> g >> x;
			while (1) {
				problem pr = x == 1 ? *Type[g].rbegin() : *Type[g].begin();
				if (isSolved(pr)) Type[g].erase(pr);
				else break;
			}
			cout << get<1>(x == 1 ? *Type[g].rbegin() : *Type[g].begin()) << '\n';
		}
		if (op == "recommend2") {
			int x;
			cin >> x;
			while (1) {
				problem pr = x == 1 ? *Total.rbegin() : *Total.begin();
				if (isSolved(pr)) Total.erase(pr);
				else break;
			}
			cout << get<1>(x == 1 ? *Total.rbegin() : *Total.begin()) << '\n';
		}
		if (op == "recommend3") {
			int x, l;
			cin >> x >> l;
			bool f = 0;
			if (x == 1) {
				for (int i = l; i <= 100; i++) {
					while (!Rank[i].empty()) {
						problem pr = *Rank[i].begin();
						if (isSolved(pr)) Rank[i].erase(pr);
						else { f = 1; break; }
					}
					if (f) { cout << get<1>(*Rank[i].begin()) << '\n'; break; }
				}
				if (!f) cout << "-1\n";
			}
			else {
				for (int i = l - 1; i > 0; i--) {
					while (!Rank[i].empty()) {
						problem pr = *Rank[i].rbegin();
						if (isSolved(pr)) Rank[i].erase(pr);
						else { f = 1; break; }
					}
					if (f) { cout << get<1>(*Rank[i].rbegin()) << '\n'; break; }
				}
				if (!f) cout << "-1\n";
			}
		}
		if (op == "add") {
			int p, l, g;
			cin >> p >> l >> g;
			problem pr = { l,p,g,numToId[p] = id++ };
			Total.insert(pr);
			Type[g].insert(pr);
			Rank[l].insert(pr);
		}
		if (op == "solved") {
			int p;
			cin >> p;
			solved[numToId[p]] = 1;
		}
	}

}

```

### [Java]

```java

import java.util.*;
import java.io.*;

class Problem{
	int num, type, rank, id;
	Problem(int num, int type, int rank, int id){
		this.num = num;
		this.type = type;
		this.rank = rank;
		this.id = id;
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
	static TreeSet<Problem> Total = new TreeSet<>((a,b) -> {
		if(a.rank == b.rank) return a.num-b.num;
		return a.rank-b.rank;
	});
	static TreeSet<Problem>[] Type = new TreeSet[101];
	static TreeSet<Problem>[] Rank = new TreeSet[101];
	static boolean[] vis = new boolean[200001];
	static int id = 0;
	static int N;
	static int[] numToId = new int[200001];
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		for(int i=1;i<=100;i++) {
			Type[i] = new TreeSet<>((a,b) -> {
				if(a.rank == b.rank) return a.num-b.num;
				return a.rank-b.rank;
			});
			Rank[i] = new TreeSet<>((a,b) -> {
				if(a.rank == b.rank) return a.num-b.num;
				return a.rank-b.rank;
			});
		}
		for(int i=0;i<N;i++) {
			nextLine();
			int p = nextInt(), l = nextInt(), g = nextInt();
			Problem now = new Problem(p, g, l, id);
			numToId[p] = id++;
			Total.add(now);
			Type[g].add(now);
			Rank[l].add(now);
		}
		
		
	}
	
	static void solve() throws Exception{

		int M = Integer.parseInt(br.readLine());
		while(M-- > 0) {
			nextLine();
			String op = st.nextToken();
			if(op.equals("recommend")) {
				int g = nextInt(), x = nextInt();
				if(x == 1) {
					while(true) {
						Problem now = Type[g].last();
						if(vis[now.id]) Type[g].pollLast();
						else break;
					}
					bw.write(Type[g].last().num + "\n");
				}
				else {
					while(true) {
						Problem now = Type[g].first();
						if(vis[now.id]) Type[g].pollFirst();
						else break;
					}
					bw.write(Type[g].first().num + "\n");
				}
			}
			
			if(op.equals("recommend2")) {
				int x = nextInt();
				if(x == 1) {
					while(true) {
						Problem now = Total.last();
						if(vis[now.id]) Total.pollLast();
						else break;
					}
					bw.write(Total.last().num + "\n");
				}
				else {
					while(true) {
						Problem now = Total.first();
						if(vis[now.id]) Total.pollFirst();
						else break;
					}
					bw.write(Total.first().num + "\n");
				}
			}
			
			if(op.equals("recommend3")) {
				int x = nextInt(), l = nextInt();
				boolean find = false;
				if(x == 1) {
					for(int i=l;i<=100;i++) {
						while(!Rank[i].isEmpty()) {
							Problem now = Rank[i].first();
							if(vis[now.id]) Rank[i].pollFirst();
							else {
								find = true;
								break;
							}
						}
						if(find) {
							bw.write(Rank[i].first().num + "\n");
							break;
						}
					}
					if(!find) bw.write("-1\n");
				}
				else {
					for(int i=l-1;i>0;i--) {
						while(!Rank[i].isEmpty()) {
							Problem now = Rank[i].last();
							if(vis[now.id]) Rank[i].pollLast();
							else {
								find = true;
								break;
							}
						}
						if(find) {
							bw.write(Rank[i].last().num + "\n");
							break;
						}
					}
					if(!find) bw.write("-1\n");
				}
			}
			
			if(op.equals("add")) {
				int p = nextInt(), l = nextInt(), g = nextInt();
				Problem pr = new Problem(p, g, l, id);
				numToId[p] = id++;
				Total.add(pr);
				Type[g].add(pr);
				Rank[l].add(pr);
			}
			
			if(op.equals("solved")) {
				int p = nextInt();
				vis[numToId[p]] = true;
			}
			
		}
		
		
	}
	
}

```
