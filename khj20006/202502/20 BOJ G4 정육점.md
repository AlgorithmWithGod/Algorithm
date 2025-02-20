```cpp

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
using ll = long long;
int main()
{
	cin.tie(0)->sync_with_stdio(0);

	ll N, M;
	cin >> N >> M;
	vector<pair<ll, ll>> A(N);
	for (auto &[x, y] : A) cin >> y >> x;
	sort(A.begin(), A.end(), [](auto a, auto b) -> bool {
		if (a.first == b.first) return a.second > b.second;
		return a.first < b.first;
	});
	
	ll s = 0, ans = (ll)3e9;
	for (int i = 0; i < N; ) {
		if (s + A[i].second >= M) ans = min(ans, A[i].first);
		ll p = A[i].first, temp = 0;
		while (i < N && A[i].first == p) {
			s += A[i++].second;
			temp += p;
			if (s >= M) ans = min(ans, temp);
		}
	}

	cout << (ans == (ll)3e9 ? -1 : ans);
	
}

```
