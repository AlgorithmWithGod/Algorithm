```cpp

#include <iostream>
#include <algorithm>
using namespace std;
using ll = long long;

int N;
ll A[30]{}, D;

ll R[14348907][3]{};
int S[2]{};

void half(int k, int s, int e) {
	for (int i = s; i < e; i++) {
		ll a = A[i];
		int T = S[k];
		int id = 0, id1 = 0, id2 = 0, id3 = 0;
		while (id1 < T) {
			ll r1 = R[id1][k] - a, r2 = R[id2][k], r3 = R[id3][k] + a, mn = min({ r1,r2,r3 });
			R[id++][2] = mn;
			if (mn == r1) id1++;
			else if (mn == r2) id2++;
			else id3++;
		}
		while (id2 < T) {
			ll r2 = R[id2][k], r3 = R[id3][k] + a, mn = min(r2, r3);
			R[id++][2] = mn;
			if (mn == r2) id2++;
			else id3++;
		}
		S[k] *= 3;
		while (id3 < T) R[id++][2] = R[id3++][k] + a;
		for (int j = 0; j < id; j++) R[j][k] = R[j][2];
	}
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N;
	for (int i = 0; i < N; i++) cin >> A[i];
	cin >> D;

	S[0] = S[1] = 1;
	half(0, 0, N >> 1);
	half(1, N >> 1, N);

	ll ans = 0;
	int s = S[1] - 1, e = S[1] - 1;
	for (int i = 0; i < S[0]; i++) {
		ll a = R[i][0];
		while (s >= 0 && R[s][1] >= -D - a) s--;
		while (e >= 0 && R[e][1] > D - a) e--;
		ans += e - s;
	}
	cout << ans;

}

```
