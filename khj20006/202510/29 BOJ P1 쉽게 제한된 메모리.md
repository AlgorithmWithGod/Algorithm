```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

const ll MOD = 1'000'000'007;
ll N, X, A, B, Q, ans = 0, s[100]{}, e[100]{};
vector<int> q, p;

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> X >> A >> B >> Q;
	q.resize(Q);
	p.resize(Q);
	iota(p.begin(), p.end(), 0);
	for (int& i : q) cin >> i, i++;
	fill(e, e + Q, MOD - 1);
	sort(q.begin(), q.end());
	
	int rem = Q;
	while (rem) {
		vector<int> ms;
		for (int i = 0; i < Q; i++) if (s[i] < e[i]) ms.push_back((s[i] + e[i] + 1) >> 1);
		sort(ms.begin(), ms.end());
		ms.erase(unique(ms.begin(), ms.end()), ms.end());
		vector<int> cnt(ms.size());

		int pos = 0;
		for (ll x = X, j = 0; j < N - 1; j++) {
			int d = upper_bound(ms.begin(), ms.end(), x) - ms.begin();
			if (d != ms.size()) cnt[d]++;
			x = (x * A + B) % MOD;
		}
		for (int i = 1; i < ms.size(); i++) cnt[i] += cnt[i - 1];
		
		for (int i = 0; i < Q; i++) if (s[i] < e[i]) {
			int m = (s[i] + e[i] + 1) >> 1;
			int idx = lower_bound(ms.begin(), ms.end(), m) - ms.begin();
			if (cnt[idx] < q[i]) s[i] = m;
			else e[i] = m - 1;
			if (s[i] >= e[i]) ans += (s[i] + e[i] + 1) >> 1, rem--;
		}
	}

	cout << ans;

}
```
