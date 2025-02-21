```cpp

#include <iostream>
#include <vector>
#include <algorithm>
#include <numeric>
using namespace std;

int N, M, Q;
int r[200001]{}, dep[200001]{};
int D[200001][18]{}, X[200001][18]{};
vector<vector<pair<int, int>>> V(200001);

int f(int x) { return x == r[x] ? x : r[x] = f(r[x]); }

void dfs(int n, int p, int d) {
	D[n][0] = p, dep[n] = d;
	for (auto[i, c] : V[n]) if (i != p) dfs(i, n, d + 1), X[i][0] = c;
}

void make() {
	for (int k = 1; k < 18; k++) for (int i = 1; i <= N; i++) {
		D[i][k] = D[D[i][k - 1]][k - 1];
		X[i][k] = min(X[i][k - 1], X[D[i][k - 1]][k - 1]);
	}
}

int solve(int a, int b) {
	if (dep[a] < dep[b]) swap(a, b);
	int diff = dep[a] - dep[b], res = 2e9;
	for (int i = 0; i < 18; i++) if (diff & (1 << i)) {
		res = min(res, X[a][i]);
		a = D[a][i];
	}
	if (a == b) return res;
	while (D[a][0] != D[b][0]) {
		for (int i = 0; i < 18; i++) if (D[a][i] == D[b][i]) {
			i--;
			res = min({ res, X[a][i], X[b][i] });
			a = D[a][i], b = D[b][i];
			break;
		}
	}
	return min({ res, X[a][0], X[b][0] });
}

int main()
{
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M >> Q;
	vector<tuple<int, int, int>> E(M);
	for (auto &[v, x, y] : E) cin >> x >> y >> v;
	sort(E.begin(), E.end(), greater<>());
	
	iota(r, r + N + 1, 0);
	for (auto[v, a, b] : E) {
		int x = f(a), y = f(b);
		if (x == y) continue;
		r[x] = y;
		V[a].emplace_back(b, v);
		V[b].emplace_back(a, v);
	}

	dfs(1, 0, 0);
	make();

	for (int a, b; Q--;) {
		cin >> a >> b;
		cout << solve(a, b) << '\n';
	}

}

```
