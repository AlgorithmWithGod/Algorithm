```cpp

#include <iostream>
#include <vector>
#include <algorithm>
#include <set>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace std;
using namespace __gnu_pbds;
using ll = long long;

int seg[262145][2]{};

#define ordered_set tree<ll, null_type, less_equal<ll>, rb_tree_tag, tree_order_statistics_node_update>
ordered_set os;

void upt(int s, int e, int i, int n, int x) {
	if (s == e) {
		seg[n][x]++;
		return;
	}
	int m = (s + e) >> 1;
	if (i <= m) upt(s, m, i, n * 2, x);
	else upt(m + 1, e, i, n * 2 + 1, x);
	seg[n][x]++;
}

int find(int s, int e, int l, int r, int n, int x) {
	if (l > r || l > e || r < s) return 0;
	if (l <= s && e <= r) return seg[n][x];
	int m = (s + e) >> 1;
	return find(s, m, l, r, n * 2, x) + find(m + 1, e, l, r, n * 2 + 1, x);
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	int N;
	cin >> N;

	vector<vector<int>> in(100001), out(100001);
	int H[200001]{};

	vector<pair<int, int>> V;
	for (int i = 1, a, b; i <= N; i++) {
		cin >> a >> b;
		in[a].push_back(i);
		out[b].push_back(i);
		V.emplace_back(a, b);
		upt(1, 100000, a, 1, 0);
		upt(1, 100000, b, 1, 1);

	}

	int s1 = 0;
	sort(V.begin(), V.end(), [](auto a, auto b) -> bool {
		if (a.second == b.second) return a.first > b.first;
		return a.second < b.second;
	});

	for (int i=0;i<V.size();i++) {
	    while(i<V.size()-1 && V[i].first == V[i+1].first){
	        os.insert(V[i++].first);
	    }
	    int a = V[i].first, b = V[i].second;
		int res = find(1, 100000, a, b-1, 1, 0) + find(1, 100000, a+1, b, 1, 1) - 1;

        
		res -= (os.size() - os.order_of_key(a));
		os.insert(a);

		s1 = max(s1, res);
	}


	set<int> S = { 0 };
	int s2 = 0, mex = 0;
	for (int x = 1; x <= 100000; x++) {
		for (int i : out[x]) {
			S.erase(H[i]);
			mex = min(mex, H[i]);
		}
		for (int i : in[x]) {
			while (S.count(mex)) mex++;
			S.insert(H[i] = mex++);
		}
		s2 = max(s2, *S.rbegin());
	}

	cout << s1 << ' ' << s2;

}

```
