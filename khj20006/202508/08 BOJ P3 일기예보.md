```cpp
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace std;
using namespace __gnu_pbds;

using ll = long long;
using pbds = tree<ll, null_type, less_equal<ll>, rb_tree_tag, tree_order_statistics_node_update>;

pbds os;
ll a[100001]{};
int N, M;

void remove(ll v) {
	os.erase(os.find_by_order(os.order_of_key(v)));
}

int main(){
	cin.tie(0)->sync_with_stdio(0);

	cin>>N>>M;
	for(int i=1;i<=N;i++) {
		cin>>a[i];
		os.insert(a[i]);
	}

	for(;M--;) {
		int o;
		cin>>o;
		if(o <= 2) {
			int i;
			ll x;
			cin>>i>>x;
			x *= o == 1 ? 1 : -1;
			remove(a[i]);
			a[i] += x;
			os.insert(a[i]);
		}
		else if(o == 3) {
			ll l, r;
			cin>>l>>r;
			cout<<os.order_of_key(r+1) - os.order_of_key(l)<<'\n';
		}
		else {
			int t;
			cin>>t;
			t = N-t+1;
			ll s = 0, e = 2e15, m = (s+e+1)>>1;
			while(s<e) {
				if(os.order_of_key(m) < t) s = m;
				else e = m-1;
				m = (s+e+1)>>1;
			}
			cout<<m<<'\n';
		}
	}

}
```
