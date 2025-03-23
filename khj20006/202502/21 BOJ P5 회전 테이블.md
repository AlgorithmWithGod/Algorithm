```cpp

#include <iostream>
#include <queue>
#include <tuple>
#include <algorithm>
using namespace std;
using ll = long long;

ll N;
ll S[3]{};
ll A[101][3]{};
ll dp[101][101][101][3][2]{};

// 시계 (b -> a)
ll cal1(ll a, ll b) { return b >= a ? b - a : b + N - a; }
// 반시계 (b -> a)
ll cal2(ll a, ll b) { return a >= b ? a - b : a + N - b; }

int main()
{
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	int K = N / 3;
	for (int i = 0; i < 3; i++) {
		cin >> S[i];
		for (int j = 1; j <= S[i]; j++) {
			cin >> A[j][i];
			if (i == 1) A[j][i] = (A[j][i] + 2 * K) % N;
			else if (i == 2) A[j][i] = (A[j][i] + K) % N;
			if (A[j][i] == 0) A[j][i] = N;
		}
	}

	dp[1][0][0][0][0] = cal1(A[1][0], 1);
	dp[1][0][0][0][1] = cal2(A[1][0], 1);
	dp[0][1][0][1][0] = cal1(A[1][1], 1);
	dp[0][1][0][1][1] = cal2(A[1][1], 1);
	dp[0][0][1][2][0] = cal1(A[1][2], 1);
	dp[0][0][1][2][1] = cal2(A[1][2], 1);

	for (int a = 0; a <= S[0]; a++) for (int b = 0; b <= S[1]; b++) for (int c = 0; c <= S[2]; c++) {
		if (a + b + c <= 1) continue;
		ll &res1 = dp[a][b][c][0][0];
		ll &res2 = dp[a][b][c][0][1];
		ll &res3 = dp[a][b][c][1][0];
		ll &res4 = dp[a][b][c][1][1];
		ll &res5 = dp[a][b][c][2][0];
		ll &res6 = dp[a][b][c][2][1];
		res1 = 1e18;
		res2 = 1e18;
		res3 = 1e18;
		res4 = 1e18;
		res5 = 1e18;
		res6 = 1e18;

		if (a > 0) {
			ll t1 = min(dp[a - 1][b][c][0][0], dp[a - 1][b][c][0][1]);
			ll t2 = min(dp[a - 1][b][c][1][0], dp[a - 1][b][c][1][1]);
			ll t3 = min(dp[a - 1][b][c][2][0], dp[a - 1][b][c][2][1]);

			ll v1 = 1e18;
			if (a - 1 > 0) res1 = min(res1, t1 + cal1(A[a][0], A[a - 1][0]));
			if (b > 0) res1 = min(res1, t2 + cal1(A[a][0], A[b][1]));
			if (c > 0) res1 = min(res1, t3 + cal1(A[a][0], A[c][2]));
			ll v2 = 1e18;
			if (a - 1 > 0) res2 = min(res2, t1 + cal2(A[a][0], A[a - 1][0]));
			if (b > 0) res2 = min(res2, t2 + cal2(A[a][0], A[b][1]));
			if (c > 0) res2 = min(res2, t3 + cal2(A[a][0], A[c][2]));
		}
		if (b > 0) {
			ll t1 = min(dp[a][b - 1][c][0][0], dp[a][b - 1][c][0][1]);
			ll t2 = min(dp[a][b - 1][c][1][0], dp[a][b - 1][c][1][1]);
			ll t3 = min(dp[a][b - 1][c][2][0], dp[a][b - 1][c][2][1]);

			ll v1 = 1e18;
			if (a > 0) res3 = min(res3, t1 + cal1(A[b][1], A[a][0]));
			if (b - 1 > 0) res3 = min(res3, t2 + cal1(A[b][1], A[b - 1][1]));
			if (c > 0) res3 = min(res3, t3 + cal1(A[b][1], A[c][2]));
			ll v2 = 1e18;
			if (a > 0) res4 = min(res4, t1 + cal2(A[b][1], A[a][0]));
			if (b - 1 > 0) res4 = min(res4, t2 + cal2(A[b][1], A[b - 1][1]));
			if (c > 0) res4 = min(res4, t3 + cal2(A[b][1], A[c][2]));
		}
		if (c > 0) {
			ll t1 = min(dp[a][b][c - 1][0][0], dp[a][b][c - 1][0][1]);
			ll t2 = min(dp[a][b][c - 1][1][0], dp[a][b][c - 1][1][1]);
			ll t3 = min(dp[a][b][c - 1][2][0], dp[a][b][c - 1][2][1]);

			ll v1 = 1e18;
			if (a > 0) res5 = min(res5, t1 + cal1(A[c][2], A[a][0]));
			if (b > 0) res5 = min(res5, t2 + cal1(A[c][2], A[b][1]));
			if (c - 1 > 0) res5 = min(res5, t3 + cal1(A[c][2], A[c - 1][2]));
			ll v2 = 1e18;
			if (a > 0) res6 = min(res6, t1 + cal2(A[c][2], A[a][0]));
			if (b > 0) res6 = min(res6, t2 + cal2(A[c][2], A[b][1]));
			if (c - 1 > 0) res6 = min(res6, t3 + cal2(A[c][2], A[c - 1][2]));
		}

	}

	ll ans = 2e18;
	for (int i = 0; i < 3; i++) for (int j = 0; j < 2; j++) ans = min(ans, dp[S[0]][S[1]][S[2]][i][j]);
	cout << ans;

}

```
