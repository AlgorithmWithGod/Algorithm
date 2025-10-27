```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M, A, B, C, D;
int arr[1002][1002]{}, brr[1002][1002]{}, crr[1002][1002]{}, drr[1002][1002]{}, err[1002][1002]{};

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> M >> N >> B >> A >> D >> C;
	for (int i = 1; i <= N; i++) for (int j = 1; j <= M; j++) {
		cin >> arr[i][j];
		arr[i][j] += arr[i - 1][j] + arr[i][j - 1] - arr[i - 1][j - 1];
	}

	for (int i = 1; i <= N - A + 1; i++) for (int j = 1; j <= M - B + 1; j++) {
		brr[i][j] = arr[i + A - 1][j + B - 1] - arr[i - 1][j + B - 1] - arr[i + A - 1][j - 1] + arr[i - 1][j - 1];
	}

	for (int i = 1; i <= N - C + 1; i++) for (int j = 1; j <= M - D + 1; j++) {
		crr[i][j] = arr[i + C - 1][j + D - 1] - arr[i - 1][j + D - 1] - arr[i + C - 1][j - 1] + arr[i - 1][j - 1];
	}

	// crr에서 세로 A-2-C+1, 가로 B-2-D+1 만큼의 최솟값 구하기
	for (int i = 2; i < N - C + 1; i++) {
		deque<pair<int, int>> dq;
		for (int j = 2; j < M - D + 1; j++) {
			while (!dq.empty() && dq.back().first > crr[i][j]) dq.pop_back();
			dq.emplace_back(crr[i][j], j);
			while (!dq.empty() && j - dq.front().second > B - 2 - D + 1) dq.pop_front();
			drr[i][j] = dq.front().first;
		}
	}

	for (int j = 2; j < M - D + 1; j++) {
		deque<pair<int, int>> dq;
		for (int i = 2; i < N - C + 1; i++) {
			while (!dq.empty() && dq.back().first > drr[i][j]) dq.pop_back();
			dq.emplace_back(drr[i][j], i);
			while (!dq.empty() && i - dq.front().second > A - 2 - C + 1) dq.pop_front();
			err[i][j] = dq.front().first;
		}
	}

	int ans = -1;
	int w = -1, x = -1;
	for (int i = 1; i <= N - A + 1; i++) for (int j = 1; j <= M - B + 1; j++) {
		int res = arr[i][j] - err[i + 1][j + 1];
		if (res > ans) {
			w = i, x = j;
			ans = res;
		}
	}
	int y = -1, z = -1;
	for (int i = w + 1; i <= w + A - 2 - C + 1; i++) for (int j = x + 1; j <= x + B - 2 - D + 1; j++) {
		if (err[i][j] == arr[i - 1][j - 1] - ans) {
			return cout << x << ' ' << w << '\n' << j << ' ' << i, 0;
		}
	}


}
``
