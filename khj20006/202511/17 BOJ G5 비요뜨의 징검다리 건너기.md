```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

ll MOD = 1e9 + 7;

ll power(ll a) {
	if (a <= 1) return (1 << a);
	ll h = power(a >> 1) % MOD;
	h = h * h % MOD;
	return (a & 1) ? h * 2 % MOD : h;
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	ll T, N, MOD = 1e9 + 7;
	for (cin >> T; T--;) {
		cin >> N;
		cout << (N <= 2 ? 1 : power(N - 2)) << '\n';
	}

}
```
