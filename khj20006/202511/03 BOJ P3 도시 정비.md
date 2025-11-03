```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int N;
vector<vector<int>> v(1000001);
ll inmx[1000001]{}, outmx[1000001]{}, ex[1000001]{}, val[1000001]{}, a[1000001]{};
ll ans = 0;

void dfs1(int n, int p) {
	inmx[n] = a[n];
	ll mx1 = 0, mx2 = 0;
	for (int i : v[n]) if (i != p) {
		dfs1(i, n);
		if (inmx[i] > mx1) mx2 = mx1, mx1 = inmx[i];
		else if (inmx[i] > mx2) mx2 = inmx[i];
		inmx[n] = max(inmx[n], inmx[i]);
	}
	for (int i : v[n]) if (i != p) {
		if (inmx[i] == mx1) ex[i] = mx2;
		else ex[i] = mx1;
		val[n] += inmx[i];
	}
}

void dfs2(int n, int p) {
	outmx[n] = max({ outmx[p], (ll)a[p], ex[n] });
	ans = max(ans, val[n] + outmx[n]);
	for (int i : v[n]) if (i != p) dfs2(i, n);
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	for (int i = 1; i <= N; i++) cin >> a[i];
	for (int i = 1, c, d; i < N; i++) {
		cin >> c >> d;
		v[c].push_back(d);
		v[d].push_back(c);
	}
	dfs1(1, 0);
	dfs2(1, 0);

	cout << ans;

}
```
