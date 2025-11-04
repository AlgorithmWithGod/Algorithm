```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M;
char arr[1000][1000]{};
int dp[1000][1000]{};

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M;
	int x = 0, y = 0;
	for (int i = 0; i < N; i++) for (int j = 0; j < M; j++) {
		cin >> arr[i][j];
		if (arr[i][j] == 'R') x = i, y = j;
	}
	for (int i = 0; i < N; i++) for (int j = 0; j <= y; j++) dp[i][j] = -1;
	dp[x][y] = 0;
	for (int j = y + 1; j < M; j++) for (int i = 0; i < N; i++) {
		if (arr[i][j] == '#') {
			dp[i][j] = -1;
			continue;
		}
		dp[i][j] = -1;
		int c = arr[i][j] == 'C' ? 1 : 0;
		if (dp[i][j - 1] != -1) dp[i][j] = dp[i][j - 1] + c;
		if (i > 0 && dp[i - 1][j - 1] != -1) dp[i][j] = max(dp[i][j], dp[i - 1][j - 1] + c);
		if (i < N - 1 && dp[i + 1][j - 1] != -1) dp[i][j] = max(dp[i][j], dp[i + 1][j - 1] + c);
	}

	int ans = -1;
	for (int i = 0; i < N; i++) for (int j = 0; j < M; j++) if (arr[i][j] == 'O') ans = max(ans, dp[i][j]);
	cout << ans;

}
```
