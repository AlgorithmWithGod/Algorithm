```cpp

#include <iostream>
#include <queue>
#include <tuple>
#include <algorithm>
using namespace std;

int dx[4] = { 1,0,-1,0 };
int dy[4] = { 0,1,0,-1 };
int N, M, sx, sy;
char A[700][700]{};
int L[700][700]{}, X[700][700]{};

int main()
{
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M;
	queue<tuple<int, int, int>> Q;
	bool vis[700][700]{};
	for (int i = 0; i < N; i++) for (int j = 0; j < M; j++) {
		cin >> A[i][j];
		if (A[i][j] == 'V') Q.emplace(i, j, 0), vis[i][j] = 1;
		if (A[i][j] == 'Y') sx = i, sy = j;
	}

	for (int i = 0; i < N; i++)	for (int j = 0; j < M; j++) X[i][j] = 2e9;
	while (!Q.empty()) {
		auto[x, y, t] = Q.front();
		Q.pop();
		X[x][y] = min(X[x][y], t);
		for (int k = 0; k < 4; k++) {
			int xx = x + dx[k], yy = y + dy[k];
			while (0 <= xx && xx < N && 0 <= yy && yy < M && A[xx][yy] != 'I') {
				X[xx][yy] = min(X[xx][yy], t);
				xx += dx[k], yy += dy[k];
			}
			xx = x + dx[k], yy = y + dy[k];
			if (xx < 0 || xx >= N || yy < 0 || yy >= M || A[xx][yy] == 'I' || vis[xx][yy]) continue;
			vis[xx][yy] = 1;
			Q.emplace(xx, yy, t + 1);
		}
	}

	for (int i = 0; i < N; i++) for (int j = 0; j < M; j++) vis[i][j] = 0;
	vis[sx][sy] = 1;
	Q.emplace(sx, sy, 0);
	while (!Q.empty()) {
		auto[x, y, t] = Q.front();
		Q.pop();
		if (A[x][y] == 'T') return cout << "YES", 0;
		for (int k = 0; k < 4; k++) {
			int xx = x + dx[k], yy = y + dy[k];
			if (xx < 0 || xx >= N || yy < 0 || yy >= M || A[xx][yy] == 'I' || vis[xx][yy] || t + 1 >= X[xx][yy]) continue;
			Q.emplace(xx, yy, t + 1);
			vis[xx][yy] = 1;
		}
	}
	cout << "NO";

}

```
