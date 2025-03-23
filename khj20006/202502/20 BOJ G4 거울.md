```cpp

#include <iostream>
#include <algorithm>
using namespace std;

int A[1002][1002]{}, N, M, ans[4001]{};
int dx[2] = { -1,0 };
int dy[2] = { 0,1 };

int main()
{
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M;
	for (int i = 1; i <= N; i++) for (int j = 1; j <= M; j++) cin >> A[i][j];

	int cnt = 0;
	for (int i = 1; i <= N; i++) A[i][0] = ++cnt;
	for (int j = 1; j <= M; j++) A[N + 1][j] = ++cnt;
	for (int i = N; i >= 1; i--) A[i][M + 1] = ++cnt;
	for (int j = M; j >= 1; j--) A[0][j] = ++cnt;

	for (int cur = 1; cur <= N + M; cur++) {
		int x = min(N, cur), y = max(1, cur - N), dir = cur <= N;
		while (1 <= x && x <= N && 1 <= y && y <= M) {
			if (A[x][y]) dir ^= 1;
			x += dx[dir], y += dy[dir];
		}

		int from = cur, to = A[x][y];
		ans[from] = to;
		ans[to] = from;
	}
	
	for (int i = 1; i <= cnt; i++) cout << ans[i] << ' ';
	
}

```
