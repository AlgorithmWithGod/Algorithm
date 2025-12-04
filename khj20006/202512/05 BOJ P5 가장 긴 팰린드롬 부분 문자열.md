```cpp
#include <bits/stdc++.h>
using namespace std;

string t, s = "#";
int A[222222]{}, C = 1, R = 1;

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> t;
	for (char i : t) s += i, s += "#";
	
	int ans = 0;
	for (int i = 1; i < s.size(); i++) {
		A[i] = min(A[2 * C - i], R - i);
		while (i > A[i] && i + A[i] + 1 < s.size() && s[i - A[i] - 1] == s[i + A[i] + 1]) A[i]++;
		if (i + A[i] >= R) C = i, R = i + A[i];
		ans = max(ans, A[i]);
	}
	cout << ans;

}
```
