```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M, S, P;
vector<vector<int>> g(500001), r(500001), rv(500001);
bitset<500001> rt;
bitset<500001> rest;
bitset<500001> vis;
int m[500001]{}, c[500001]{}, mn[500001]{}, d[500001]{}, dp[500001]{};
stack<int> st;
set<pair<int, int>> ch;

void dfs1(int n) {
	for (int i : g[n]) if (!vis[i]) {
		vis[i] = 1;
		dfs1(i);
	}
	st.push(n);
}

int dfs2(int n, int t) {
	c[n] = t;
	int sum = m[n];
	for (int i : r[n]) if (!vis[i]) {
		vis[i] = 1;
		sum += dfs2(i, t);
	}
	return sum;
}

void dfs3(int n) {
	for (int i : rv[n]) {
		d[i]++;
		if (!vis[i]) {
			vis[i] = 1;
			dfs3(i);
		}
	}
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M;
	for (int i = 0, a, b; i < M; i++) {
		cin >> a >> b;
		g[a].push_back(b);
		r[b].push_back(a);
	}
	for (int i = 1; i <= N; i++) cin >> m[i];
	cin >> S >> P;
	for (int a; P--; rt[a] = 1) cin >> a;

	for (int i = 1; i <= N; i++) if (!vis[i]) {
		vis[i] = 1;
		dfs1(i);
	}
	vis.reset();
	int cnt = 0;
	while (!st.empty()) {
		int n = st.top(); st.pop();
		if (vis[n]) continue;
		cnt++;
		vis[n] = 1;
		mn[cnt] = dfs2(n, cnt);
	}

	for (int i = 1; i <= N; i++) {
		for (int j : g[i]) if (c[i] != c[j] && !ch.count(make_pair(c[i], c[j]))) {
			rv[c[i]].push_back(c[j]);
			ch.emplace(c[i], c[j]);
		}
		if (rt[i]) rest[c[i]] = 1;
	}

	queue<int> q;
	vis.reset();
	dfs3(c[S]);
	q.push(c[S]);
	dp[c[S]] = mn[c[S]];
	int ans = 0;
	while (!q.empty()) {
		int n = q.front(); q.pop();
		if (rest[n]) ans = max(ans, dp[n]);
		for (int i : rv[n]) {
			dp[i] = max(dp[i], dp[n] + mn[i]);
			if (!--d[i]) q.push(i);
		}
	}
	cout << ans;

}
```
