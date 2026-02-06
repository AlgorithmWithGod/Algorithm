```cpp
#include <bits/stdc++.h>
using namespace std;

int R, C, H, W;
int arr[3001][3001]{}, cnt[3001][3001]{};

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> R >> C >> H >> W;
	for (int i = 1; i <= R; i++) for (int j = 1; j <= C; j++) {
		cin >> arr[i][j];
	}

	int low = 1, high = R * C, mid = (low + high) >> 1;
	while (low < high) {
		bool possible = false;
		for (int i = 1; i <= R && !possible; i++) for (int j = 1; j <= C && !possible; j++) {
			cnt[i][j] = arr[i][j] <= mid ? 1 : 0;
			cnt[i][j] += cnt[i - 1][j] + cnt[i][j - 1] - cnt[i - 1][j - 1];
			if (i >= H && j >= W) {
				int scale = cnt[i][j] - cnt[i - H][j] - cnt[i][j - W] + cnt[i - H][j - W];
				if (scale > ((H * W) >> 1)) {
					possible = true;
					break;
				}
			}
		}
		if (possible) {
			high = mid;
		}
		else {
			low = mid + 1;
		}
		mid = (low + high) >> 1;
	}
	cout << mid;
	
}
```
