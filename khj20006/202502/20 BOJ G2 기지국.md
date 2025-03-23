```cpp

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
using ll = long long;

int main()
{
	cin.tie(0)->sync_with_stdio(0);

	int N;
	ll inf = 1e18;
	cin >> N;
	vector<pair<ll, ll>> A(N);
	for (auto &[x, y] : A) cin >> x >> y;
	sort(A.begin(), A.end());

	vector<ll> dp(10000, inf);
	dp[0] = abs(A[0].second) * 2;
	for (int i = 1; i < N; i++) {
		int p = i;
		ll maxabs = -1;
		while (i < N && A[p].first == A[i].first) maxabs = max(maxabs, abs(A[i++].second));
		i--;
		for (int j = p - 1; j >= 0; j--) {
			maxabs = max(maxabs, abs(A[j+1].second));
			dp[i] = min(dp[i], dp[j] + max(maxabs * 2, A[i].first - A[j + 1].first));
		}
		maxabs = max(maxabs, abs(A[0].second));
		dp[i] = min(dp[i], max(maxabs * 2, A[i].first - A[0].first));
	}
	cout << dp[N - 1];

}

```
