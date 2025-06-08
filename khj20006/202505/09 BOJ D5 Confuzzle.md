```cpp
#include <iostream>
#include <vector>
#include <map>
#include <utility>
#include <algorithm>
using namespace std;

int N, INF = 1e9 + 7, ans = INF, C[100001]{};
vector<vector<int>> V(100001);
map<int, pair<int, int>> M[100001]{};

void dfs(int n, int p) {
	for (int i : V[n]) if (i != p) {
		dfs(i, n);
		C[i]++;
		if (M[i].size() > M[n].size()) swap(M[i], M[n]), swap(C[i], C[n]);
		for (auto[c, d] : M[i]) {
			auto[fir, sec] = d;
			if (M[n].find(c) == M[n].end()) M[n][c] = { fir + C[i] - C[n], sec + C[i] - C[n] };
			else {
				if (fir + C[i] < M[n][c].first + C[n]) M[n][c].second = M[n][c].first, M[n][c].first = fir + C[i] - C[n];
				else if (fir < M[n][c].second) M[n][c].second = fir + C[i] - C[n];
				if (sec < M[n][c].second) M[n][c].second = sec + C[i] - C[n];
			}
			ans = min(ans, M[n][c].first + M[n][c].second + 2*C[n]);
		}
		M[i] = map<int, pair<int, int>>();
	}
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	for (int i = 1, a; i <= N; i++) {
		cin >> a;
		M[i][a] = { 0,INF };
	}
	for (int i = 1, a, b; i < N; i++) {
		cin >> a >> b;
		V[a].push_back(b);
		V[b].push_back(a);
	}

	dfs(1, 0);
	cout << ans;

}
```
