```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M;
vector<vector<int>> G(200001), R(200001);
bitset<200001> vis;
int last, cnt = 0;

void dfs1(int n) {
	for (int i : G[n]) if (!vis[i]) {
		vis[i] = 1;
		dfs1(i);
	}
	last = n;
}

void dfs2(int n) {
	cnt++;
	for (int i : R[n]) if (!vis[i]) {
		vis[i] = 1;
		dfs2(i);
	}
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M;
	for (int a, b; M--;) {
		cin >> a >> b;
		G[a].push_back(b);
		R[b].push_back(a);
	}

	for (int i = 1; i <= N; i++) if (!vis[i]) {
		vis[i] = 1;
		dfs1(i);
	}

	vis.reset();
	vis[last] = 1;
	dfs2(last);
	cout << (cnt == N ? "Yes" : "No");

}
```
