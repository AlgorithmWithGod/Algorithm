```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

const ll MOD = 1e9 + 7;
ll N, M;

ll power(ll a, ll b) {
	if (b == 0) return 1;
	if (b == 1) return a % MOD;
	ll h = power(a, b >> 1) % MOD;
	h = h * h % MOD;
	return (b & 1) ? h * a % MOD : h;
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M;
	N = (1 << N);
	if (M > N) return cout << 1, 0;

	ll g = power(N, M), p = 1;
	for (ll i = N; i > N - M; i--) p = (p * i) % MOD;

	ll ans = ((g - p + MOD) % MOD) * power(g, MOD - 2) % MOD;
	cout << ans;

}
```
