```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

const ll MOD = 1e9 + 7;

ll power(ll b) {
    if(b == 0) return 1;
    if(b == 1) return 2;
    ll h = power(b>>1) % MOD;
    h = (h*h)%MOD;
    return (b&1) ? h * 2 % MOD : h;
}

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    ll N;
    cin>>N;
    cout<<(N == 0 ? 0 : power(N-1) % MOD);
    
}
```
