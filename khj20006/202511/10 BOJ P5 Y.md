```cpp
#include <bits/stdc++.h>
using namespace std;

int N;
vector<vector<int>> v(100001);
int d[100001]{}, dd[100001]{}, u[100001]{};
int ans = 0;

void dfs(int n, int p) {
	int mx1 = 0, mx2 = 0, mx3 = 0;
	for (int i : v[n]) if (i != p) {
		dfs(i, n);
		int res = d[i] + 1;
		if (res > mx1) mx3 = mx2, mx2 = mx1, mx1 = res;
		else if (res > mx2) mx3 = mx2, mx2 = res;
		else if (res > mx3) mx3 = res;
	}
	d[n] = mx1, dd[n] = mx2;
	if (mx3) ans = max(ans, mx1 + mx2 + mx3 + 1);
}

void dfs2(int n, int p) {
	if (n != 1) u[n] = max(u[p], d[p] == d[n] + 1 ? dd[p] : d[p]) + 1;
	if (u[n] && dd[n]) ans = max(ans, d[n] + dd[n] + u[n] + 1);
	for (int i : v[n]) if (i != p) dfs2(i, n);
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	for (int i = 1, a, b; i < N; i++) {
		cin >> a >> b;
		v[a].push_back(b);
		v[b].push_back(a);
	}
	dfs(1, 0);
	dfs2(1, 0);
	cout << ans;

}
```
