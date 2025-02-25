```cpp

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
using ll = long long;

int N, Q;
vector<vector<int>> V(100001);
int par[100001][17]{}, dep[100001]{};

void dfs(int n, int p, int d) {
	par[n][0] = p, dep[n] = d;
	for (int i : V[n]) if (i != p) dfs(i, n, d + 1);
}

void makeTable() {
	for (int k = 1; k < 17; k++) for (int i = 1; i <= N; i++) par[i][k] = par[par[i][k - 1]][k - 1];
}

pair<int, int> solve(int a, int b) {
	int diff = abs(dep[a] - dep[b]);
	int ma = 0, mb = 0;
	int oa = a, ob = b;
	for (int i = 0; i < 17; i++) if (diff & (1 << i)) {
		if (dep[a] > dep[b]) a = par[a][i], ma += (1 << i);
		else b = par[b][i], mb += (1 << i);
	}

	while (par[a][0] != par[b][0]) {
		for (int i = 16; i >= 0; i--) if (par[a][i] != par[b][i]) {
			a = par[a][i], ma += (1 << i);
			b = par[b][i], mb += (1 << i);
			break;
		}
	}
	if (a != b) {
		a = par[a][0], ma++;
		b = par[b][0], mb++;
	}

	int d = ma + mb;
	if (ma == mb) return { a, d };
	if ((ma + mb) % 2) return { -1,d };

	int from = ma > mb ? oa : ob, to = a, len = (ma + mb) / 2;
	for (int i = 0; i < 17; i++) if (len & (1 << i)) from = par[from][i];
	return { from, d };

}

int main()
{
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	for (int i = 1, a, b; i < N; i++) {
		cin >> a >> b;
		V[a].push_back(b);
		V[b].push_back(a);
	}

	dfs(1, 0, 0);
	makeTable();

	for (cin >> Q; Q--;) {
		int a, b, c;
		cin >> a >> b >> c;
		int res = -1;

		auto[m1, _x] = solve(a, b);
		if (m1 != -1) {
			auto[_1, l1] = solve(a, m1);
			auto[_2, l2] = solve(b, m1);
			auto[_3, l3] = solve(c, m1);
			if (l1 == l2 && l2 == l3) res = m1;
		}
		auto[m2, _y] = solve(b, c);
		if (m2 != -1) {
			auto[_1, l1] = solve(a, m2);
			auto[_2, l2] = solve(b, m2);
			auto[_3, l3] = solve(c, m2);
			if (l1 == l2 && l2 == l3) res = m2;
		}
		auto[m3, _z] = solve(a, c);
		if (m3 != -1) {
			auto[_1, l1] = solve(a, m3);
			auto[_2, l2] = solve(b, m3);
			auto[_3, l3] = solve(c, m3);
			if (l1 == l2 && l2 == l3) res = m3;
		}

		cout << res << '\n';
	}

}

```
