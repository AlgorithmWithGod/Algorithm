```cpp
#include <bits/stdc++.h>
using namespace std;

const int INF = 1e9 + 7;
int N;
int cost[1500][1500]{}, dp[1500][1500]{};

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	for (int i = 0; i < N; i++) for (int j = 0; j < N; j++) {
		cin >> cost[i][j];
		dp[i][j] = INF;
	}

	dp[0][1] = dp[1][0] = cost[0][1];
	for (int x = 1; x < N - 1; x++) {
		for (int i = 0; i < x; i++) {
			dp[x + 1][x] = min(dp[x + 1][x], dp[i][x] + cost[i][x + 1]);
			dp[i][x + 1] = min(dp[i][x + 1], dp[i][x] + cost[x][x + 1]);
			dp[x + 1][i] = min(dp[x + 1][i], dp[x][i] + cost[x][x + 1]);
			dp[x][x + 1] = min(dp[x][x + 1], dp[x][i] + cost[i][x + 1]);
		}
	}
	int ans = INF;
	for (int i = 0; i < N - 1; i++) ans = min({ ans, dp[N - 1][i], dp[i][N - 1] });
	cout << ans;
	
}
```
