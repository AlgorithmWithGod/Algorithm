### 플로이드

```cpp

#include <iostream>
#include <vector>
using namespace std;
int main()
{
	int N, M;
	cin >> N >> M;
	vector<vector<bool>> D(N + 1, vector<bool>(N + 1));
	for (int i = 1; i <= N; i++) D[i][i] = 1;
	for (int i = 0, a, b; i < M; i++) {
		cin >> a >> b;
		D[a][b] = 1;
	}

	for (int i = 1; i <= N; i++) for (int j = 1; j <= N; j++) for (int k = 1; k <= N; k++) {
		if (D[j][i] && D[i][k]) D[j][k] = 1;
	}

	int ans = 0;
	for (int i = 1; i <= N; i++) {
		int res = 0;
		for (int j = 1; j <= N; j++) res += D[i][j] + D[j][i];
		ans += res == N + 1;
	}
	cout << ans;

}

```

### 위상 정렬

```cpp

#include <iostream>
#include <vector>
#include <queue>
using namespace std;

int main()
{
	int N, M;
	cin >> N >> M;
	vector<vector<int>> V(N + 1);
	vector<vector<bool>> D(N + 1, vector<bool>(N + 1));
	vector<int> in(N + 1);
	for (int i = 1; i <= N; i++) D[i][i] = 1;
	for (int i = 0, a, b; i < M; i++) {
		cin >> a >> b;
		V[a].push_back(b);
		in[b]++;
	}

	queue<int> Q;
	for (int i = 1; i <= N; i++) if (!in[i]) Q.push(i);

	while (!Q.empty()) {
		int x = Q.front();
		Q.pop();
		for (int i : V[x]) {
			for (int j = 1; j <= N; j++) if (D[j][x]) D[j][i] = 1;
			if (!(--in[i])) Q.push(i);
		}
	}

	int ans = 0;
	for (int i = 1; i <= N; i++) {
		int res = 0;
		for (int j = 1; j <= N; j++) res += D[i][j] + D[j][i];
		ans += res == N + 1;
	}
	cout << ans;

}

```
