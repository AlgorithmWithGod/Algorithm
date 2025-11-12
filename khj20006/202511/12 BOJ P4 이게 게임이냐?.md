```cpp
#include <bits/stdc++.h>
using namespace std;

int N;
int a[51]{}, b[51]{};
int vis[111][111][122][122]{};

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	N >>= 1;
	for (int i = 1; i <= N; i++) {
		cin >> a[i] >> b[i];
		a[i] += 10;
		b[i] += 10;
	}
	queue<tuple<int, int, int, int, int>> q;
	q.emplace(0, 0, 121, 121, 1);
	vis[0][0][121][121] = 1;
	while (!q.empty()) {
		auto [c, d, e, f, t] = q.front(); q.pop();
		if (t == N + 1) return cout << "WIN", 0;
		int x = a[t], y = b[t];
		
		if ((x > c || abs(x - c) == 10) && (y > x || abs(y - x) == 10) && vis[y][d][e][f] != t + 1) {
			q.emplace(y, d, e, f, t + 1);
			vis[y][d][e][f] = t + 1;
		}
		if ((y > c || abs(y - c) == 10) && (x > y || abs(x - y) == 10) && vis[x][d][e][f] != t + 1) {
			q.emplace(x, d, e, f, t + 1);
			vis[x][d][e][f] = t + 1;
		}
		if ((x > c || abs(x - c) == 10) && (y > d || abs(y - d) == 10) && vis[x][y][e][f] != t + 1) {
			q.emplace(x, y, e, f, t + 1);
			vis[x][y][e][f] = t + 1;
		}
		if ((x > c || abs(x - c) == 10) && (y < e || abs(y - e) == 10) && vis[x][d][y][f] != t + 1) {
			q.emplace(x, d, y, f, t + 1);
			vis[x][d][y][f] = t + 1;
		}
		if ((x > c || abs(x - c) == 10) && (y < f || abs(y - f) == 10) && vis[x][d][e][y] != t + 1) {
			q.emplace(x, d, e, y, t + 1);
			vis[x][d][e][y] = t + 1;
		}

		if ((x > d || abs(x - d) == 10) && (y > x || abs(y - x) == 10) && vis[c][y][e][f] != t + 1) {
			q.emplace(c, y, e, f, t + 1);
			vis[c][y][e][f] = t + 1;
		}
		if ((y > d || abs(y - d) == 10) && (x > y || abs(x - y) == 10) && vis[c][x][e][f] != t + 1) {
			q.emplace(c, x, e, f, t + 1);
			vis[c][x][e][f] = t + 1;
		}
		if ((x > d || abs(x - d) == 10) && (y > c || abs(y - c) == 10) && vis[y][x][e][f] != t + 1) {
			q.emplace(y, x, e, f, t + 1);
			vis[y][x][e][f] = t + 1;
		}
		if ((x > d || abs(x - d) == 10) && (y < e || abs(y - e) == 10) && vis[c][x][y][f] != t + 1) {
			q.emplace(c, x, y, f, t + 1);
			vis[c][x][y][f] = t + 1;
		}
		if ((x > d || abs(x - d) == 10) && (y < f || abs(y - f) == 10) && vis[c][x][e][y] != t + 1) {
			q.emplace(c, x, e, y, t + 1);
			vis[c][x][e][y] = t + 1;
		}

		if ((x < e || abs(x - e) == 10) && (y < x || abs(y - x) == 10) && vis[c][d][y][f] != t + 1) {
			q.emplace(c, d, y, f, t + 1);
			vis[c][d][y][f] = t + 1;
		}
		if ((y < e || abs(y - e) == 10) && (x < y || abs(x - y) == 10) && vis[c][d][x][f] != t + 1) {
			q.emplace(c, d, x, f, t + 1);
			vis[c][d][x][f] = t + 1;
		}
		if ((x < e || abs(x - e) == 10) && (y > c || abs(y - c) == 10) && vis[y][d][x][f] != t + 1) {
			q.emplace(y, d, x, f, t + 1);
			vis[y][d][x][f] = t + 1;
		}
		if ((x < e || abs(x - e) == 10) && (y > d || abs(y - d) == 10) && vis[c][y][x][f] != t + 1) {
			q.emplace(c, y, x, f, t + 1);
			vis[c][y][x][f] = t + 1;
		}
		if ((x < e || abs(x - e) == 10) && (y < f || abs(y - f) == 10) && vis[c][d][x][y] != t + 1) {
			q.emplace(c, d, x, y, t + 1);
			vis[c][d][x][y] = t + 1;
		}

		if ((x < f || abs(x - f) == 10) && (y < x || abs(y - x) == 10) && vis[c][d][e][y] != t + 1) {
			q.emplace(c, d, e, y, t + 1);
			vis[c][d][e][y] = t + 1;
		}
		if ((y < f || abs(y - f) == 10) && (x < y || abs(x - y) == 10) && vis[c][d][e][x] != t + 1) {
			q.emplace(c, d, e, x, t + 1);
			vis[c][d][e][x] = t + 1;
		}
		if ((x < f || abs(x - f) == 10) && (y > c || abs(y - c) == 10) && vis[y][d][e][x] != t + 1) {
			q.emplace(y, d, e, x, t + 1);
			vis[y][d][e][x] = t + 1;
		}
		if ((x < f || abs(x - f) == 10) && (y > d || abs(y - d) == 10) && vis[c][y][e][x] != t + 1) {
			q.emplace(c, y, e, x, t + 1);
			vis[c][y][e][x] = t + 1;
		}
		if ((x < f || abs(x - f) == 10) && (y < e || abs(y - e) == 10) && vis[c][d][y][x] != t + 1) {
			q.emplace(c, d, y, x, t + 1);
			vis[c][d][y][x] = t + 1;
		}

	}
	cout << "LOSE";

}
```
