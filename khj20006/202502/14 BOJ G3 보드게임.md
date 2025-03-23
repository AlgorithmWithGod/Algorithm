```cpp

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
	cin.tie(0)->sync_with_stdio(0);

	int N;
	cin >> N;
	char col[1001]{};
	for (int i = 1; i <= N; i++) cin >> col[i];

	vector<vector<pair<int, char>>> V(1001);
	int M, K;
	for (cin >> M >> K; K--;) {
		int a, b;
		char c;
		cin >> a >> b >> c;
		V[a].emplace_back(b, c);
		V[b].emplace_back(a, c);
	}

	vector<int> D(M + 1, -1);
	D[1] = 0;
	for (int t = 1; t <= N; t++) {
		vector<int> ND(M + 1, -1);
		for (int i = 1; i <= M; i++) {
			if (D[i] == -1) continue;
			for (auto &[x, c] : V[i]) {
				int val = D[i] + (c == col[t] ? 10 : 0);
				ND[x] = max(ND[x], val);
			}
		}
		D = ND;
	}
	int ans = *max_element(D.begin(), D.end());
	cout << (ans == -1 ? 0 : ans);

}

```
