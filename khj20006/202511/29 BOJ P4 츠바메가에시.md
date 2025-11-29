```cpp
#include <bits/stdc++.h>
using namespace std;

struct SegmentTree {
	vector<pair<int, int>> tree;

	pair<int, int> mrg(pair<int, int> &a, pair<int, int> &b) {
		int mx1 = 0, mx2 = 0;
		mx1 = max(a.first, b.first);
		if (mx1 == a.first) mx2 = max(a.second, b.first);
		else mx2 = max(a.first, b.second);
		return { mx1, mx2 };
	}
public:
	SegmentTree(int sz) {
		tree.resize(sz * 4);
	}

	void upt(int s, int e, int i, int v, int n) {
		if (s == e) {
			tree[n].first += v;
			return;
		}
		int m = (s + e) >> 1;
		if (i <= m) upt(s, m, i, v, n << 1);
		else upt(m + 1, e, i, v, n << 1 | 1);
		tree[n] = mrg(tree[n << 1], tree[n << 1 | 1]);
	}
};

int N;
SegmentTree* segX = new SegmentTree(1000001);
SegmentTree* segY = new SegmentTree(1000001);
vector<pair<int, int>> X[1000001];
vector<pair<int, int>> Y[1000001];

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	for (int i = 0, x, y, v; i < N; i++) {
		cin >> x >> y >> v;
		X[x].emplace_back(y, v);
		Y[y].emplace_back(x, v);
		segX->upt(0, 1000000, x, v, 1);
		segY->upt(0, 1000000, y, v, 1);
	}

	int ans = 0;
	int xmx1 = 0, xmx2 = 0, xmx3 = 0;
	for (int x = 0; x <= 1000000; x++) {
		int sum = 0;
		for (auto [y, v] : X[x]) {
			segY->upt(0, 1000000, y, -v, 1);
			sum += v;
		}
		auto [a, b] = segY->tree[1];
		ans = max(ans, sum + a + b);
		for (auto [y, v] : X[x]) {
			segY->upt(0, 1000000, y, v, 1);
		}
		if (sum > xmx1) xmx3 = xmx2, xmx2 = xmx1, xmx1 = sum;
		else if (sum > xmx2) xmx3 = xmx2, xmx2 = sum;
		else if (sum > xmx3) xmx3 = sum;
	}
	ans = max(ans, xmx1 + xmx2 + xmx3);

	int ymx1 = 0, ymx2 = 0, ymx3 = 0;
	for (int y = 0; y <= 1000000; y++) {
		int sum = 0;
		for (auto [x, v] : Y[y]) {
			segX->upt(0, 1000000, x, -v, 1);
			sum += v;
		}
		auto [a, b] = segX->tree[1];
		ans = max(ans, sum + a + b);
		for (auto [x, v] : Y[y]) {
			segX->upt(0, 1000000, x, v, 1);
		}
		if (sum > ymx1) ymx3 = ymx2, ymx2 = ymx1, ymx1 = sum;
		else if (sum > ymx2) ymx3 = ymx2, ymx2 = sum;
		else if (sum > ymx3) ymx3 = sum;
	}
	ans = max(ans, ymx1 + ymx2 + ymx3);

	cout << ans;

}
```
