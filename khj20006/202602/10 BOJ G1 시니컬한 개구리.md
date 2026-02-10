```cpp
#include <bits/stdc++.h>
using namespace std;
const int INF = 1234567;

const int dx[4] = { 1,0,-1,0 };
const int dy[4] = { 0,1,0,-1 };

int N, M, rf, cf, rh, ch;
vector<vector<vector<pair<int, int>>>> fgraph(1000, vector<vector<pair<int, int>>>(1000));
vector<vector<vector<pair<int, int>>>> rgraph(1000, vector<vector<pair<int, int>>>(1000));

vector<vector<int>> bfs(pair<int, int> start, vector<vector<vector<pair<int, int>>>> &graph) {
	vector<vector<int>> dist(N, vector<int>(M, INF));
	queue<tuple<int, int, int>> q;
	dist[start.first][start.second] = 0;
	q.emplace(start.first, start.second, 0);
	while (!q.empty()) {
		auto [x, y, t] = q.front();
		q.pop();
		for (auto [xx, yy] : graph[x][y]) {
			if (dist[xx][yy] > dist[x][y] + 1) {
				dist[xx][yy] = dist[x][y] + 1;
				q.emplace(xx, yy, dist[xx][yy]);
			}
		}
	}
	return dist;
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M >> rf >> cf >> rh >> ch;
	rf--, cf--, rh--, ch--;
	for (int i = 0; i < N; i++) for (int j = 0, a; j < M; j++) {
		cin >> a;
		for (int k = 0; k < 4; k++) {
			int x = i + dx[k] * a, y = j + dy[k] * a;
			if (x < 0 || x >= N || y < 0 || y >= M) continue;
			fgraph[i][j].emplace_back(x, y);
			rgraph[x][y].emplace_back(i, j);
		}
	}

	vector<vector<int>> fdist = bfs({ rf, cf }, fgraph);
	vector<vector<int>> rdist = bfs({ rh, ch }, rgraph);

	int ans = fdist[rh][ch];
	for (int i = 0; i < N; i++) {
		int fmin = INF, rmin = INF;
		for (int j = 0; j < M; j++) {
			fmin = min(fmin, fdist[i][j]);
			rmin = min(rmin, rdist[i][j]);
		}
		ans = min(ans, fmin + rmin + 1);
	}

	for (int j = 0; j < M; j++) {
		int fmin = INF, rmin = INF;
		for (int i = 0; i < N; i++) {
			fmin = min(fmin, fdist[i][j]);
			rmin = min(rmin, rdist[i][j]);
		}
		ans = min(ans, fmin + rmin + 1);
	}
	cout << (ans == INF ? -1 : ans);

}
```