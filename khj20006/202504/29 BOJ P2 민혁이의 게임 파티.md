```cpp
#include <iostream>
#include <numeric>
#include <set>
using namespace std;

int N, M, Q;
multiset<int> S[100001]{};
int A[100001]{}, C[100001]{}, r[100001]{}, ans[100001]{};

int f(int x) { return x == r[x] ? x : r[x] = f(r[x]); }

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M >> Q;
	for (int i = 1; i <= N; i++) {
		cin >> A[i];
		S[i].insert(A[i]);
		C[A[i]]++;
	}
	for (int i = 1; i <= M; i++) ans[i] = C[i] == 1 ? 0 : -1;

	iota(r, r + N + 1, 0);

	for (int a, b, t = 1; Q--; t++) {
		cin >> a >> b;
		int x = f(a), y = f(b);
		if (x == y) continue;
		if (S[x].size() > S[y].size()) swap(x, y);
		for (int j : S[x]) {
			S[y].insert(j);
			if (C[j] == S[y].count(j) && ans[j] < 0) ans[j] = t;
		}
		S[x] = multiset<int>();
		r[x] = y;
	}

	for (int i = 1; i <= M; i++) cout << ans[i] << '\n';

}
```
