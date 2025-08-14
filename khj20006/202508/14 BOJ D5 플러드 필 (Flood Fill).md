```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

ll INF = 1e12;

ll N, D;
int r[100000]{}, c[100000]{};
pair<ll,ll> a[100000]{};
set<tuple<ll,ll,int>> s;

int f(int x) {return x==r[x] ? x : r[x]=f(r[x]);}

int main(){
	cin.tie(0)->sync_with_stdio(0);

	cin>>N>>D;
	iota(r, r+N, 0);
	fill(c, c+N, 1);
	for(int i=0;i<N;i++) {
		ll x, y;
		cin>>x>>y;
		a[i] = {y+x, y-x};
	}

	sort(a, a+N);
	priority_queue<tuple<ll,ll,ll,int>, vector<tuple<ll,ll,ll,int>>, greater<>> pq;
	for(int j=0;j<N;j++) {
		auto [x,y] = a[j];
		while(!pq.empty() && get<0>(pq.top()) <= x) {
			auto [_a, _b, _c, _d] = pq.top();
			pq.pop();
			s.erase({_b,_c,_d});
		}
		auto it = s.upper_bound({y, -INF, -1});
		if(it != s.end() && get<0>(*it) <= y+D) {
			int p = f(j), q = f(get<2>(*it));
			if(p != q) {
				c[p] += c[q];
				r[q] = p;
			}

		}
		if(it != s.begin()) {
			it--;
			if(get<0>(*it) >= y-D) {
				int p = f(j), q = f(get<2>(*it));
				if(p != q) {
					c[p] += c[q];
					r[q] = p;
				}
			}
		}
		
		s.emplace(y,x,j);
		pq.emplace(x+D+1,y,x,j);
	}

	int cnt = 0, mx = 0;
	bitset<100000> v;
	for(int i=0;i<N;i++) {
		int x = f(i);
		if(v[x]) continue;
		v[x] = 1;
		mx = max(mx, c[x]);
		cnt++;
	}
	cout<<cnt<<' '<<mx;

}
```
