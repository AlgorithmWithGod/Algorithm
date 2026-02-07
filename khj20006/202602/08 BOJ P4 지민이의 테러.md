```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;
using point = pair<ll, ll>;

struct line {
	point src, dest;
	line(point a, point b) {
		if (a > b) {
			swap(a, b);
		}
		src = a, dest = b;
	}
};

int N;
vector<point> points;

int ccw(point a, point b, point c) {
	auto [ax, ay] = a;
	auto [bx, by] = b;
	auto [cx, cy] = c;
	ll ret = (ax * by + bx * cy + cx * ay) - (ax * cy + bx * ay + cx * by);
	return ret == 0 ? 0 : (ret > 0 ? 1 : -1);
}

bool line_intersection(line n1, line n2) {
	auto [n1_src, n1_dest] = n1;
	auto [n2_src, n2_dest] = n2;
	int res1 = ccw(n1_src, n1_dest, n2_src) * ccw(n1_src, n1_dest, n2_dest);
	int res2 = ccw(n2_src, n2_dest, n1_src) * ccw(n2_src, n2_dest, n1_dest);
	if (res1 == 0 && res2 == 0) {
		return n1_src <= n2_dest && n2_src <= n1_dest;
	}
	return res1 <= 0 && res2 <= 0;
}

bool point_in_polygon(point p) {
	line n1 = line({ 1e9 + 1, 1e9 + 2 }, p);
	bool ret = 0;
	for (int i = 0; i < N; i++) {
		line n2 = line(points[i], points[(i + 1) % N]);
		if (ccw(p, n2.src, n2.dest) == 0 && n2.src <= p && p <= n2.dest) {
			return true;
		}
		ret ^= line_intersection(n1, n2);
	}
	return ret;
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	points.resize(N);
	for (auto& [x, y] : points) {
		cin >> x >> y;
	}

	for (int i = 0, x, y; i < 3; i++) {
		cin >> x >> y;
		cout << point_in_polygon({ x, y }) << '\n';
	}

}
```
