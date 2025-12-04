```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int N, K;
ll dp[100001]{}, s[100001]{};
deque<pair<ll, int>> d;

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> K;
	for (int i = 1, a; i <= N; i++) {
		cin >> a;
		s[i] = s[i - 1] + a;
	}

	ll ans = 0;
	d.emplace_back(s[N], -1);
	d.emplace_back(s[N] - s[1], 0);
	for (int i = 1; i <= N; i++) {
		while (!d.empty() && i - d.front().second > K + 1) d.pop_front();
		int idx = d.front().second;
		dp[i] = (idx >= 0 ? dp[idx] : 0) + s[i] - s[idx + 1];

		ans = max(ans, dp[i]);
		if (i < N) {
			ll val = dp[i] + s[N] - s[i + 1];
			while (!d.empty() && d.back().first <= val) d.pop_back();
			d.emplace_back(val, i);
		}
	}
	cout << ans;

}
```
