```cpp

#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>
using namespace std;
using ll = long long;

int D[32]{1};

int sol(int d, int s, int e);
int ans(int x, int y);

int main()
{
	cin.tie(0)->sync_with_stdio(0);

	for (int i = 1; i < 32; i++) D[i] = D[i - 1] + i;
	int T, x, y;
	for (cin >> T; T--;) {
		cin >> x >> y;
		cout << ans(x, y) << '\n';
	}

}

int J(int x) {
	if (x <= 1) return x;
	int lg = log2(x);
	if (x == (1 << (lg + 1)) - 1) return lg + 1;
	if (x == (1 << (lg + 1)) - 2) return lg * 2;
	return lg + J(x - (1 << lg) + 1);
}

int sol(int d, int s, int e) {
	if (s == e) return J(s + (1 << d) - 1);
	if (e == (1 << d)) {
		int res = max(d * 2, d + 1);
		if (s == (1 << d) - 1) return res;
		return max(res, d + ans(s, e - 2));
	}
	return d + ans(s, e);
}

int ans(int x, int y) {
	if (y <= 5) {
		int arr[6] = { 0,1,2,2,3,4 };
		int mx = 0;
		for (int i = x; i <= y; i++) mx = max(mx, arr[i]);
		return mx;
	}
	int depX = log2(x);
	int depY = log2(y);
	int idxX = x - (1 << depX) + 1;
	int idxY = y - (1 << depY) + 1;
	if (depY - depX > 1) return max(D[depY - 1], sol(depY, 1, idxY));
	if (depY - depX == 1) return max(sol(depY, 1, idxY), sol(depX, idxX, (1 << depX)));
	return sol(depX, idxX, idxY);
}

```
