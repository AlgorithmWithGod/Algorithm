```cpp

#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int main()
{
	cin.tie(0)->sync_with_stdio(0);

	int N;
	for (cin >> N; N; cin >> N) {

		vector<int> A;
		int ans = 0;
		for (int i = 1; i*i <= N; i++) A.push_back(i*i);
		int M = A.size();

		// 1
		if (A.back() == N) ans++;
		// 2
		for (int i = 0; i < M; i++) for (int j = i; j < M; j++) if (A[i] + A[j] == N) ans++;
		// 3
		for (int i = 0; i < M; i++) for (int j = i; j < M; j++) {
			if (A[i] + A[j] >= N) break;
			ans += upper_bound(A.begin() + j, A.end(), N - A[i] - A[j]) - lower_bound(A.begin() + j, A.end(), N - A[i] - A[j]);
		}
		// 4
		for (int i = 0; i < M; i++) for (int j = i; j < M; j++) for (int k = j; k < M; k++) {
			if (A[i] + A[j] + A[k] >= N) break;
			ans += upper_bound(A.begin() + k, A.end(), N - A[i] - A[j] - A[k]) - lower_bound(A.begin() + k, A.end(), N - A[i] - A[j] - A[k]);
		}

		cout << ans << '\n';
	}
	
}

```
