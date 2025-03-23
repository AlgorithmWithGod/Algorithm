```cpp

#include <iostream>
#include <tuple>
#include <queue>
using namespace std;

int N, M, P, A[1000][1000]{}, S[10]{};
int dx[4] = { 1,0,-1,0 };
int dy[4] = { 0,1,0,-1 };

int main()
{
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M >> P;
	for (int i = 1; i <= P; i++) cin >> S[i];
	for (int i = 0; i < N; i++) for (int j = 0; j < M; j++) {
		char a;
		cin >> a;
		if (a == '.') continue;
		if (a == '#') A[i][j] = -1;
		else A[i][j] = a - '0';
	}

	queue<tuple<int, int, int>> Q[10]{};
	for (int p = 1; p <= P; p++) {
		for (int i = 0; i < N; i++) for (int j = 0; j < M; j++) if (A[i][j] == p) Q[p].emplace(i, j, S[p]);
	}

	while (true) {

		bool change = false;
		queue<tuple<int, int, int>> NQ[10]{};
		for (int p = 1; p <= P; p++) {
			while (!Q[p].empty()) {
				auto[x, y, t] = Q[p].front();
				Q[p].pop();
				for (int k = 0; k < 4; k++) {
					int xx = x + dx[k], yy = y + dy[k];
					if (xx < 0 || xx >= N || yy < 0 || yy >= M || A[xx][yy]) continue;
					change = true;
					A[xx][yy] = p;
					if (t > 1)	Q[p].emplace(xx, yy, t - 1);
					else NQ[p].emplace(xx, yy, S[p]);
				}
			}
		}
		if (!change) break;
		for (int p = 1; p <= P; p++) Q[p] = NQ[p];

	}

	int cnt[10]{};
	for (int i = 0; i < N; i++) for (int j = 0; j < M; j++) for (int p = 1; p <= P; p++) cnt[p] += A[i][j] == p;
	for (int i = 1; i <= P; i++) cout << cnt[i] << ' ';

}

```
