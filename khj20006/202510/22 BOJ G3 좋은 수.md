```cpp
#include <bits/stdc++.h>
using namespace std;

int N, a[5000]{};
bitset<400001> v;

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	int ans = 0;
	for (int i = 0; i < N; i++) {
		cin >> a[i];
		int res = 0;
		for (int j = 0; j < i; j++) {
			if (v[a[i] - a[j] + 200000]) res = 1;
		}
		for (int j = 0; j <= i; j++) v[a[i] + a[j] + 200000] = 1;
		ans += res;
	}
	cout << ans;

}
```
