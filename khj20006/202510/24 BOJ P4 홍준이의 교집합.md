```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

ll N, K;
const ll MOD = 1e9 + 7;
vector<pair<ll, int>> events;
ll c[200001]{};

ll power(ll a, ll b) {
	if (b == 0) return 1;
	if (b == 1) return a % MOD;
	ll h = power(a, b >> 1);
	h = (h * h) % MOD;
	return (b & 1) ? h * a % MOD : h;
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> K;

	c[K] = 1;
	for (int x = 1; K + x <= N; x++) c[K + x] = c[K + x - 1] * (K + x) % MOD * power(x, MOD - 2) % MOD;

	for (int i = 0, l, r; i < N; i++) {
		cin >> l >> r;
		events.emplace_back(l, 1);
		events.emplace_back(r + 1, -1);
	}

	sort(events.begin(), events.end());
	
	ll ans = 0, prev = MOD, cnt = 0;
	for (int i = 0; i < N * 2;) {
		ll prevCnt = cnt, cur = events[i].first;
		while (i < N * 2 && events[i].first == cur) cnt += events[i++].second;
		if (prev != MOD) ans = (ans + (cur - prev) * c[prevCnt]) % MOD;
		prev = cur;
	}
	cout << ans;

}
```
