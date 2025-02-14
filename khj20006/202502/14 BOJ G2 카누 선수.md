```cpp

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
	cin.tie(0)->sync_with_stdio(0);

	int T;
	for (cin >> T; T--;) {
		int K, N;
		cin >> K >> N;
		vector<int> A(N), B(N), C(N), D(N);
		vector<int> R1, R2;
		for (int &i : A) cin >> i;
		for (int &i : B) cin >> i;
		for (int &i : C) cin >> i;
		for (int &i : D) cin >> i;
		for (int i : A)for (int j : B) R1.push_back(i + j);
		for (int i : C)for (int j : D) R2.push_back(i + j);


		int ans = 2e9, diff = 2e9;
		sort(R2.begin(), R2.end());
		for (int i : R1) {
			int p = lower_bound(R2.begin(), R2.end(), K - i) - R2.begin();
			
			if (p < R2.size()) {
				int v = abs(R2[p] + i-K);
				if (v < diff) diff = v, ans = R2[p] + i;
                else if(v == diff) ans = min(ans, R2[p] + i);
			}
			if (0 <= p-1 && p-1 <= R2.size()) {
				int v = abs(R2[p - 1] + i-K);
				if (v < diff) diff = v, ans = R2[p-1] + i;
                else if(v == diff) ans = min(ans, R2[p-1] + i);
			}
		}
		cout << ans << '\n';

	}

}

```
