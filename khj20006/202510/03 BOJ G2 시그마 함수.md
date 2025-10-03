```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

ll N;

unordered_set<ll> m;
bitset<1000001> e;
vector<ll> p = {2};

void bck(ll n) {
    for(ll i:p) {
        if((__int128)n*i > (__int128)N) break;
        if(m.count(n*i)) continue;
        m.insert(n*i);
        bck(n*i);
    }
}

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    for(int i=2;i*i<=1000000;i++) if(!e[i]) for(int j=i*i;j<=1000000;j+=i) e[j] = 1;
    for(ll i=3;i<=1000000;i++) if(!e[i]) p.push_back(i*i);

    cin>>N;
    m.insert(1);
    bck(1);
    
    cout<<N-m.size()<<'\n';

}
```
