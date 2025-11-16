```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M, a[20]{}, ans = -1234567;

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M;
	for (int i = 0; i < N; i++) cin >> a[i];

	for (int i = 1; i < (1 << N); i++) {
		int sum = 0, group = 0, cnt = 0;
		for (int j = 0; j < N; j++) {
			if ((i & (1 << j))) {
				cnt++;
				if ((!j || !(i & (1 << (j - 1))))) group++;
			}
			sum += (i & (1 << j)) ? a[j] : 0;
		}
		if (group <= M && cnt >= M) ans = max(ans, sum);
	}
	cout << ans;

}
```
