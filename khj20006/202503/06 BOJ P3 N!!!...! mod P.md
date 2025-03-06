```java

#include <iostream>
using namespace std;
using ll = long long;

ll N, K, P;

ll power(ll n, ll m){
    if(m == 0) return 1;
    if(m == 1) return n;
    ll p = power(n,m>>1);
    if(m&1) return p*p%P*n%P;
    return p*p%P;
}

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> K >> P;

	if (N == 2) return cout << (P == 2 ? 0 : 2), 0;

	if (K >= 4) return cout << 0, 0;

	if (K == 2) {
		if (N >= 13) return cout << 0, 0;
        ll fac = 1;
        for (int i = 1; i <= N; i++) fac *= i;
        if (fac >= P) return cout << 0, 0;
        if(N <= 11){
            ll ans = 1;
            for(int i=2;i<=fac;i++) ans = (ans * i) % P;
            return cout<<ans,0;
        }

        ll res = 1;
        for(int i=479001601;i<P;i++) res = (res * i) % P;

        cout<<(P-1) * power(res,P-2) % P;

	}

	if (K == 3) {
		if (N >= 4) return cout << 0, 0;
		ll ans = 1;
		for (int i = 1; i <= 720; i++) ans = (ans * i) % P;
		cout << ans;
	}

}

```
