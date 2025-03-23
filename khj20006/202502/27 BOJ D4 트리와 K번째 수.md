```cpp

#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>
using namespace std;
#define AA(p,q,s)	p.begin(), p.end(), q.begin(), q.end(), s.begin()
int A[100001]{}, par[100001]{}, sz[100001]{}, dep[100001]{}, cn[100001]{}, ci[100001]{};
vector<vector<int>> V(100001), C(100001);
vector<vector<int>> seg[100001]{};

int dfs(int n, int p) {
	par[n] = p, sz[n] = 1;
	for (int i : V[n]) if (i != p) sz[n] += dfs(i, n);
	return sz[n];
}

void hld(int n, int p, int s, int d) {
	dep[n] = d, cn[n] = s, ci[n] = C[s].size();
	C[s].push_back(n);
	int h = -1;
	for (int i : V[n]) if (i != p && (h == -1 || sz[i] > sz[h])) h = i;
	if (h != -1) hld(h, n, s, d);
	for (int i : V[n]) if (i != p && i != h) hld(i, n, i, d + 1);
}

void init(int id, int s, int e, int n) {
	if (s == e) {
		seg[id][n] = { A[C[id][s]] };
		return;
	}
	int m = (s + e) >> 1;
	init(id, s, m, n * 2);
	init(id, m + 1, e, n * 2 + 1);
	seg[id][n].resize(seg[id][n * 2].size() + seg[id][n * 2 + 1].size());
	merge(AA(seg[id][n * 2], seg[id][n * 2 + 1], seg[id][n]));
}

int find(int id, int s, int e, int l, int r, int k, int n) {
	if (l > r || l > e || r < s) return 0;
	if (l <= s && e <= r) return lower_bound(seg[id][n].begin(), seg[id][n].end(), k) - seg[id][n].begin();
	int m = (s + e) >> 1;
	return find(id, s, m, l, r, k, n * 2) + find(id, m + 1, e, l, r, k, n * 2 + 1);
}

int cnt(int a, int b, int k) {
	int res = 0;
	while (cn[a] != cn[b]) {
		if (dep[a] > dep[b]) {
			res += find(cn[a], 0, C[cn[a]].size() - 1, 0, ci[a], k, 1);
			a = par[cn[a]];
		}
		else {
			res += find(cn[b], 0, C[cn[b]].size() - 1, 0, ci[b], k, 1);
			b = par[cn[b]];
		}
	}
	if (ci[a] > ci[b]) swap(a, b);
	res += find(cn[a], 0, C[cn[a]].size() - 1, ci[a], ci[b], k, 1);
	return res;
}

int M[100000]{};

int main() {
	cin.tie(0)->sync_with_stdio(0);

	int N, Q;
	cin >> N >> Q;
	vector<pair<int, int>> Value;
	for (int i = 1; i <= N; i++) {
		cin >> A[i];
		Value.emplace_back(A[i], i);
	}
	sort(Value.begin(), Value.end());
	for (int i = 0; i < N; i++) M[i] = Value[i].first, A[Value[i].second] = i;


	for (int i = 1, a, b; i < N; i++) {
		cin >> a >> b;
		V[a].push_back(b);
		V[b].push_back(a);
	}

	dfs(1, 0);
	hld(1, 0, 1, 0);

	for (int i = 1; i <= N; i++) if (!C[i].empty()) {
		seg[i].resize((1 << ((int)log2(C[i].size()) + 2)) + 1);
		init(i, 0, C[i].size() - 1, 1);
	}

	for (int x, y, k; Q--;) {
		cin >> x >> y >> k;
		long long s = 0, e = 100000, m = (s + e + 1) >> 1;
		while (s < e) {
			if (cnt(x, y, m) < k) s = m;
			else e = m - 1;
			m = (s + e + 1) >> 1;
		}
		cout << M[m] << '\n';
	}

}

```
