```cpp
#include <bits/stdc++.h>
using namespace std;

const int INF = 1e9 + 7;

int N, K, M;
vector<vector<int>> v(101001);

int bfs01(int start, int end) {
	vector<int> dist(101001, INF);
	deque<pair<int, int>> q;
	dist[start] = 1;
	q.emplace_back(1, start);
	while (!q.empty()) {
		auto [d, n] = q.front(); q.pop_front();
		for (int i : v[n]) {
			int cost = i > N ? 0 : 1;
			if (dist[i] > d + cost) {
				dist[i] = d + cost;
				if (cost) q.emplace_back(dist[i], i);
				else q.emplace_front(dist[i], i);
			}
		}
	}
	return dist[end] == INF ? -1 : dist[end];
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> K >> M;
	for (int i = 1; i <= M; i++) {
		for (int j = 1, a; j <= K; j++) {
			cin >> a;
			v[a].push_back(N + i);
			v[N + i].push_back(a);
		}
	}

	cout << bfs01(1, N);

}
```
