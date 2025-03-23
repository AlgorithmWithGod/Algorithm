```cpp

#include <iostream>
#include <vector>
#include <algorithm>
#include <numeric>
using namespace std;
using ll = long long;

int M, N, Q;

int r[250000]{}, H[500][500]{};
vector<vector<pair<int, int>>> V(250000);
int dep[250000]{}, par[250000][18]{}, cost[250000][18]{};

int f(int x) { return x == r[x] ? x : r[x] = f(r[x]); }
int coord(int x, int y) { return x * M + y; }

void makeTable() {
	for (int k = 1; k < 18; k++) for (int i = 0; i < N*M; i++) {
		par[i][k] = par[par[i][k - 1]][k - 1];
		cost[i][k] = max(cost[i][k - 1], cost[par[i][k - 1]][k - 1]);
	}
}

void dfs(int n, int p, int d) {
	par[n][0] = p, dep[n] = d;
	for (auto[i, c] : V[n]) if (i != p) {
		cost[i][0] = c;
		dfs(i, n, d + 1);
	}
}

int solve(int a, int b) {
	int res = 0;
	if (dep[a] < dep[b]) swap(a, b);
	int diff = dep[a] - dep[b];
	for (int i = 0; i < 18; i++) if (diff & (1 << i)) {
		res = max(res, cost[a][i]);
		a = par[a][i];
	}

	while (par[a][0] != par[b][0]) {
		for (int i = 17; i >= 0; i--) if (par[a][i] != par[b][i]) {
			res = max({ res, cost[a][i], cost[b][i] });
			a = par[a][i];
			b = par[b][i];
		}
	}
	if (a != b) res = max({ res, cost[a][0], cost[b][0] });

	return res;

}

int main()
{
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M >> Q;

	iota(r, r + N * M, 0);
	vector<tuple<int, int, int>> E;
	for (int i = 0; i < N; i++) for (int j = 0; j < M; j++) {
		cin >> H[i][j];
		int cur = coord(i, j);
		if (i > 0) E.emplace_back(max(H[i - 1][j], H[i][j]), cur, coord(i - 1, j));
		if (j > 0) E.emplace_back(max(H[i][j - 1], H[i][j]), cur, coord(i, j - 1));
	}

	sort(E.begin(), E.end());
	for (auto[c, a, b] : E) {
		int x = f(a), y = f(b);
		if (x == y) continue;
		V[a].emplace_back(b, c);
		V[b].emplace_back(a, c);
		r[x] = y;
	}

	dfs(0, -1, 0);
	makeTable();

	for (int a, b, c, d; Q--;) {
		cin >> a >> b >> c >> d;
		int s = coord(a - 1, b - 1), e = coord(c - 1, d - 1);

		if (s == e) cout << H[a - 1][b - 1] << '\n';
		else  cout << solve(s, e) << '\n';
	}

}

```
