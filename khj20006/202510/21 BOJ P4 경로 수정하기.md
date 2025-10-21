```cpp
#include <bits/stdc++.h>
using namespace std;

int N, Q;
int U = 0, D = 0, L = 0, R = 0, X = 0, Y = 0;

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> Q;
	for (int i = 0; i < N; i++) {
		char a;
		cin >> a;
		if (a == 'U') U++, Y++;
		if (a == 'D') D++, Y--;
		if (a == 'L') L++, X--;
		if (a == 'R') R++, X++;
	}

	for (int x, y; Q--;) {
		cin >> x >> y;
		int xDiff = abs(x - X), yDiff = abs(y - Y);
		if (abs(x) + abs(y) > N || (x + y) % 2 != (X + Y) % 2) {
			cout << "-1\n";
			continue;
		}
		cout << (xDiff + yDiff) / 2 << '\n';
	}

}
```
