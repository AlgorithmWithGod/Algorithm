```cpp
#include <bits/stdc++.h>
using namespace std;

int T, N;
vector<int> seg, arr, cnt, cnt2;
vector<pair<int, int>> arr2;

void upt(int s, int e, int i, int v, int n) {
	if (s == e) {
		seg[n] = v;
		return;
	}
	int m = (s + e) >> 1;
	if (i <= m) upt(s, m, i, v, n << 1);
	else upt(m + 1, e, i, v, n << 1 | 1);
	seg[n] = max(seg[n << 1], seg[n << 1 | 1]);
}

int find(int s, int e, int l, int r, int n) {
	if (l > r || l > e || r < s) return 0;
	if (l <= s && e <= r) return seg[n];
	int m = (s + e) >> 1;
	return max(find(s, m, l, r, n << 1), find(m + 1, e, l, r, n << 1 | 1));
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	for (cin >> T; T--;) {
		cin >> N;
		seg = vector<int>(4 * N);
		arr = vector<int>(N + 1);
		cnt = vector<int>(N + 1);
		cnt2 = vector<int>(N + 1);
		arr2 = vector<pair<int, int>>();
		for (int i = 1; i <= N; i++) {
			cin >> arr[i];
			arr2.emplace_back(arr[i], i);
			cnt[i] = arr[i - 1] < arr[i] ? cnt[i - 1] + 1 : 1;
		}
		sort(arr2.begin(), arr2.end(), [](auto a, auto b) -> bool {
			if (a.first == b.first) return a.second > b.second;
			return a.first < b.first;
		});

		for (auto [x, i] : arr2) {
			cnt2[i] = find(1, N, 1, i - 1, 1) + 1;
			upt(1, N, i, cnt[i], 1);
		}
		int ans = 0;
		for (int i = 1; i <= N; i++) {
			if (arr[i - 1] < arr[i]) cnt2[i] = max(cnt2[i], cnt2[i - 1] + 1);
			ans = max(ans, cnt2[i]);
		}
		cout << ans << '\n';
	}

}
```
