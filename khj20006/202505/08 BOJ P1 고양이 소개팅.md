```cpp
#include <iostream>
#include <vector>
#include <map>
#include <algorithm>
using namespace std;
using ll = long long;

int N;
ll C[200001]{}, H[200001]{}, par[200001]{}, dist[200001]{}, V[200001]{};
map<ll, ll> M[200001]{};
vector<vector<pair<int, ll>>> T(200001);

ll ans = 0;

void dfs(int n) {
	for (auto[i, c] : T[n]) {
		dfs(i);
		V[i] += c;
		if (M[i].size() > M[n].size()) swap(M[i], M[n]), swap(V[i], V[n]);
		for (auto[d, x] : M[i]) M[n][d + V[i] - V[n]] += x;
		M[i] = map<ll, ll>();
	}
	if (H[n] != -1) {
		H[n] -= V[n];
		auto it = M[n].upper_bound(H[n]);
		if (it == M[n].begin()) return;
		it--;
		vector<ll> er;
		while (C[n] > 0) {
			ll am = min(it->second, C[n]);
			C[n] -= am;
			ans += am;
			M[n][it->first] -= am;
			if (am == it->second) er.push_back(it->first);
			if (it == M[n].begin()) break;
			it--;
		}
		for (ll i : er) M[n].erase(i);
	}
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	for (int i = 1; i <= N; i++) cin >> C[i];
	for (int i = 1; i <= N; i++) cin >> H[i];
	for (int i = 2; i <= N; i++) cin >> par[i];
	for (int i = 2; i <= N; i++) {
		cin >> dist[i];
		T[par[i]].emplace_back(i, dist[i]);
	}

	for (int i = 1; i <= N; i++) if (H[i] == -1) M[i].insert({ 0,C[i] });
	dfs(1);

	cout << ans;

}
```
