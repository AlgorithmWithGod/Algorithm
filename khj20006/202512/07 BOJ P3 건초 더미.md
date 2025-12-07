```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int N, Q;
vector<pair<int, int>> infos;
int arr[300001]{}, idx[300001]{}, cnt[300001]{}, ans[300000]{};
ll sum[300001]{};
vector<tuple<int, int, int>> queries;

void upt(int x, int v) {
	for (; x <= 300000; x += x & -x) {
		sum[x] += v;
		cnt[x]++;
	}
}

pair<ll, int> find(int x) {
	pair<ll, int> ret = { 0,0 };
	for (; x > 0; x -= x & -x) {
		ret.first += sum[x];
		ret.second += cnt[x];
	}
	return ret;
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> Q;
	for (int i = 1; i <= N; i++) {
		cin >> arr[i];
		infos.emplace_back(arr[i], i);
	}

	sort(infos.begin(), infos.end());
	for (int i = 0; i < N; i++) {
		auto [v, x] = infos[i];
		idx[x] = i + 1;
	}

	queries.resize(Q);
	for (int i = 0; i < Q; i++) {
		auto& [X, P, x] = queries[i];
		cin >> X >> P;
		x = i;
	}

	sort(queries.begin(), queries.end());

	int pos = 0;
	for (auto [X, P, x] : queries) {
		while (pos < X) {
			pos++;
			upt(idx[pos], arr[pos]);
		}
		pair<ll, int> ri = find(N);
		if (P > ri.first) {
			ans[x] = -1;
			continue;
		}
		int s = 0, e = N - 1, m = (s + e + 1) >> 1;
		while (s < e) {
			pair<ll, int> le = find(m);
			if (ri.first - le.first >= P) s = m;
			else e = m - 1;
			m = (s + e + 1) >> 1;
		}
		ans[x] = ri.second - find(m).second;
	}

	for (int i = 0; i < Q; i++) cout << ans[i] << '\n';

}
```
