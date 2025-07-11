# C++

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int N, s[500001]{}, e[500001]{}, l[500001]{}, r[500001]{};
ll h[500001]{}, v[500001]{}, ans[500001]{};

ll seg[1048576]{};

class DisjointSet {
	public:
	int r[500001]{};
	DisjointSet() {
		for(int i=1;i<=500000;i++) r[i] = i;
	}
	int f(int x) {return x==r[x] ? x : r[x]=f(r[x]);}
	void uni(int a, int b) {
		int x = f(a), y = f(b);
		if(x == y) return;
		r[x] = y;
	}
};

DisjointSet le, ri;

void prop(int s, int e, int n){
	if(seg[n]) {
		if(s != e) {
			seg[n*2] = max(seg[n*2], seg[n]);
			seg[n*2+1] = max(seg[n*2+1], seg[n]);
			seg[n] = 0;
		}
	}
}

void upt(int s, int e, int l, int r, ll v, int n) {
	prop(s, e, n);
	if (l > r || l > e || r < s) return;
	if (l <= s && e <= r) {
		seg[n] = max(seg[n], v);
		if(s != e) {
			seg[n*2] = max(seg[n*2], v);
			seg[n*2+1] = max(seg[n*2+1], v);
		}
		return;
	}
	int m = (s + e) >> 1;
	upt(s, m, l, r, v, n * 2);
	upt(m + 1, e, l, r, v, n * 2 + 1);
}

ll find(int s, int e, int i, int n) {
	prop(s,e,n);
	if(s == e) return seg[n];
	int m = (s+e)>>1;
	if(i <= m) return find(s,m,i,n*2);
	return find(m+1,e,i,n*2+1);
}

int main(){
	cin.tie(0)->sync_with_stdio(0);

	cin>>N;
	for(int i=1;i<=N;i++) {
		s[i] = i;
		e[i] = i;
		cin>>h[i];
	}
	
	stack<pair<int, int>> s1;
	for(int i=N;i>=1;i--) {
		while(!s1.empty() && s1.top().first > h[i]) {
			int x = s1.top().second;
			l[x] = i;
			s1.pop();
		}
		s1.push({h[i],i});
	}
	
	stack<pair<int, int>> s2;
	for(int i=1;i<=N;i++) {
		while(!s2.empty() && s2.top().first > h[i]) {
			int x = s2.top().second;
			r[x] = i;
			s2.pop();
		}
		s2.push({h[i],i});
	}

	vector<pair<ll,ll>> infos;
	for(int i=1;i<=N;i++) infos.push_back({h[i],i});
	sort(infos.begin(), infos.end(), [](auto a, auto b) -> bool {
		return a.first == b.first ? a.second < b.second : a.first > b.first;
	});

	bitset<500001> vis;

	for(int x=0;x<N;) {
		ll height = infos[x].first;
		vector<pair<ll,ll>> li;
		while(x<N && height == infos[x].first) {
			int idx = infos[x].second;
			vis[idx] = 1;
			li.push_back(infos[x++]);
			if(idx>1 && vis[idx-1]) {
				le.uni(idx, idx-1);
				ri.uni(idx-1, idx);
			}
			if(idx<N && vis[idx+1]) {
				le.uni(idx+1, idx);
				ri.uni(idx, idx+1);
			}
		}

		for(auto [_,idx] : li) {
			if(idx>1 && vis[idx-1]) s[idx] = le.f(idx-1);
			else s[idx] = idx;

			if(idx<N && vis[idx+1]) e[idx] = ri.f(idx+1);
			else e[idx] = idx;

			v[idx] = height * (e[idx] - s[idx] + 1);

			upt(1,N,s[idx],idx-1,v[idx]-h[idx],1);
			upt(1,N,idx+1,e[idx],v[idx]-h[idx],1);
			upt(1,N,1,s[idx]-1,v[idx],1);
			upt(1,N,e[idx]+1,N,v[idx],1);

			if(l[idx]) {
				int L = 0;
				if(l[idx]>1 && vis[l[idx]-1]) L = le.f(l[idx]-1);
				else L = l[idx];
				ans[l[idx]] = max(ans[l[idx]], h[idx] * (e[idx] - L));
			}

			if(r[idx]) {
				int R = 0;
				if(r[idx]<N && vis[r[idx]+1]) R = ri.f(r[idx]+1);
				else R = r[idx];
				ans[r[idx]] = max(ans[r[idx]], h[idx] * (R - s[idx]));
			}
		}
	}

	for(int i=1;i<=N;i++) {
		ans[i] = max(ans[i], find(1,N,i,1));
		if(h[i] == h[i-1] && ans[i] < ans[i-1]) ans[i] = ans[i-1];
		cout<<ans[i]<<' ';
	}

}
```

# JAVA

```java
import java.util.*;
import java.io.*;

class IOController {
    BufferedReader br;
    BufferedWriter bw;
    StringTokenizer st;

    public IOController() {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer("");
    }

    String nextLine() throws Exception {
        String line = br.readLine();
        st = new StringTokenizer(line);
        return line;
    }

    String nextToken() throws Exception {
        while (!st.hasMoreTokens()) nextLine();
        return st.nextToken();
    }

    int nextInt() throws Exception {
        return Integer.parseInt(nextToken());
    }

    long nextLong() throws Exception {
        return Long.parseLong(nextToken());
    }

    double nextDouble() throws Exception {
        return Double.parseDouble(nextToken());
    }

    void close() throws Exception {
        bw.flush();
        bw.close();
    }

    void write(String content) throws Exception {
        bw.write(content);
    }

}

class DisjointSet {
    int[] r;

    DisjointSet(int size) {
        r = new int[size + 1];
        for (int i = 1; i <= size; i++) r[i] = i;
    }

    int find(int x) {
        return x == r[x] ? x : (r[x] = find(r[x]));
    }

    // a를 b에 붙임
    void union(int a, int b) {
        int x = find(a), y = find(b);
        if (x == y) return;
        r[x] = y;
    }

}

class SegTree {
    long[] tree;

    SegTree(int size) {
        tree = new long[size * 4];
    }

    void propagation(int s, int e, int n) {
        if(tree[n] != 0) {
            if(s != e) {
                tree[n*2] = Math.max(tree[n*2], tree[n]);
                tree[n*2+1] = Math.max(tree[n*2+1], tree[n]);
                tree[n] = 0;
            }
        }
    }

    void update(int s, int e, int l, int r, long v, int n) {
        propagation(s, e, n);
        if (l > r || l > e || r < s) return;
        if (l <= s && e <= r) {
            tree[n] = Math.max(tree[n], v);
            if(s != e) {
                tree[n*2] = Math.max(tree[n*2], v);
                tree[n*2+1] = Math.max(tree[n*2+1], v);
            }
            return;
        }
        int m = (s + e) >> 1;
        update(s, m, l, r, v, n * 2);
        update(m + 1, e, l, r, v, n * 2 + 1);
    }

    long find(int s, int e, int i, int n) {
        propagation(s, e, n);
        if(s == e) return tree[n];
        int m = (s+e)>>1;
        if(i <= m) return find(s,m,i,n*2);
        return find(m+1,e,i,n*2+1);
    }

}

public class Main {

    static IOController io;

    //

    static int N;
    static int[] s, e, l, r;
    static long[] h, v, ans;
    static DisjointSet left, right;
    static SegTree seg;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();
    }

    public static void init() throws Exception {

        N = io.nextInt();
        left = new DisjointSet(N + 1);
        right = new DisjointSet(N + 1);
        s = new int[N + 1];
        e = new int[N + 1];
        h = new long[N + 1];
        for (int i = 1; i <= N; i++) {
            h[i] = io.nextLong();
            s[i] = i;
            e[i] = i;
        }
        l = new int[N + 1];
        r = new int[N + 1];
        v = new long[N + 1];
        ans = new long[N+1];
        seg = new SegTree(N);

    }

    static void solve() throws Exception {

        // 정보 정렬 후 분리 집합으로 v, s, e 구하기
        // 이 때, lazy등으로 max갱신까지 같이 할 수 있으면 하기

        // l 구하기
        Stack<int[]> s1 = new Stack<>();
        for(int i=N;i>=1;i--) {
            while(!s1.isEmpty() && s1.peek()[0] > h[i]) l[s1.pop()[1]] = i;
            s1.push(new int[]{(int)h[i], i});
        }

        // r 구하기
        Stack<int[]> s2 = new Stack<>();
        for(int i=1;i<=N;i++) {
            while(!s2.isEmpty() && s2.peek()[0] > h[i]) r[s2.pop()[1]] = i;
            s2.push(new int[]{(int)h[i], i});
        }

        long[][] infos = new long[N][2];
        for (int i = 1; i <= N; i++) infos[i - 1] = new long[]{h[i], i};
        Arrays.sort(infos, (a, b) -> a[0] == b[0] ? Long.compare(a[1], b[1]) : Long.compare(b[0], a[0]));

        boolean[] vis = new boolean[N+1];

        for(int x=0;x<N;) {
            long height = infos[x][0];
            List<long[]> list = new ArrayList<>();
            while(x<N && height==infos[x][0]) {
                int idx = (int)infos[x][1];
                vis[idx] = true;
                list.add(infos[x++]);
                if(idx>1 && vis[idx-1]) {
                    left.union(idx, idx-1);
                    right.union(idx-1, idx);
                }
                if(idx<N && vis[idx+1]) {
                    left.union(idx+1, idx);
                    right.union(idx, idx+1);
                }
            }

            // 여기부터

            for(long[] info:list) {
                int idx = (int)info[1];

                if(idx>1 && vis[idx-1]) {
                    s[idx] = left.find(idx-1);
                }
                else s[idx] = idx;

                if(idx<N && vis[idx+1]) {
                    e[idx] = right.find(idx+1);
                }
                else e[idx] = idx;

                v[idx] = height * (e[idx] - s[idx] + 1);

                seg.update(1, N, s[idx], idx-1, v[idx]-h[idx], 1);
                seg.update(1, N, idx+1, e[idx], v[idx]-h[idx], 1);

                seg.update(1, N, 1, s[idx]-1, v[idx], 1);
                seg.update(1, N, e[idx]+1, N, v[idx], 1);

                if(l[idx] != 0) {
                    int L = 0;
                    if(l[idx]>1 && vis[l[idx]-1]) L = left.find(l[idx]-1);
                    else L = l[idx];
                    ans[l[idx]] = Math.max(ans[l[idx]], h[idx] * (e[idx] - L));
                }

                if(r[idx] != 0) {
                    int R = 0;
                    if(r[idx]<N && vis[r[idx]+1]) R = right.find(r[idx]+1);
                    else R = r[idx];
                    ans[r[idx]] = Math.max(ans[r[idx]], h[idx] * (R - s[idx]));
                }
            }

        }

        for(int i=1;i<=N;i++) {
            ans[i] = Math.max(ans[i], seg.find(1,N,i,1));
            if(h[i] == h[i-1] && ans[i] < ans[i-1]) ans[i] = ans[i-1];
            io.write(ans[i] + " ");
        }

    }

}
```
