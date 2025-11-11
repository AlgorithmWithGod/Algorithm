```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	cin.tie(0)->sync_with_stdio(0);

	long long T, N, M, K;
	for (cin >> T; T--;) {
		cin >> K >> N >> M;
		N--, M--;
		if (K == 1) {
			cout << (((N & 1LL) | (M & 1LL)) ? "koosaga\n" : "cubelover\n");
			continue;
		}
		long long z = min(N, M) / (K + 1), zz = z * (K + 1);
		N -= zz, M -= zz;
		long long g = (N < K || M < K) ?  ((N & 1LL) ^ (M & 1LL) ^ (z & 1LL)) : (((N & 1LL) ^ (M & 1LL)) | 2LL);
		cout << (g ? "koosaga\n" : "cubelover\n");
	}

}
```
