```cpp
#include <bits/stdc++.h>
using namespace std;

int N;
map<int, set<int>> X, Y;

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	for (int i = 0, x, y; i < N; i++) {
		cin >> x >> y;
		X[x].insert(y);
		Y[y].insert(x);
	}

	if (min(X.size(), Y.size()) <= 3) return cout << 1, 0;

	for (auto [x, v] : X) {
		for (int i : v) {
			Y[i].erase(x);
			if (Y[i].empty()) Y.erase(i);
		}
		if (Y.size() <= 2) return cout << 1, 0;
		for (int i : v) Y[i].insert(x);
	}

	for (auto [y, v] : Y) {
		for (int i : v) {
			X[i].erase(y);
			if (X[i].empty()) X.erase(i);
		}
		if (X.size() <= 2) return cout << 1, 0;
		for (int i : v) X[i].insert(y);
	}

	cout << 0;

}
```
