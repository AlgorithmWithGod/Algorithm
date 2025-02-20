```cpp

#include <iostream>
#include <algorithm>
#include <stack>
using namespace std;
using ll = long long;

int main()
{
	cin.tie(0)->sync_with_stdio(0);

	ll N, ans = 0;
	stack<ll> S;
	cin >> N;
	for (int i = 1; i <= N; i++) {
		ll a;
		cin >> a;
		if (!S.empty() && S.top() < a) {
			ll t = S.top();
			while (!S.empty() && S.top() < a) S.pop();
			ans += a - t;
		}
		S.push(a);
	}

	ans -= S.top();
	ll mx = 0;
	while (!S.empty()) mx = S.top(), S.pop();
	ans += mx;
	
	cout << ans;

}

```
