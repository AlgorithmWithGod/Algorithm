```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int N;
ll deg[300001]{};
vector<pair<int, int>> edges;

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N;
    edges.resize(N-1);
    for(auto &[a,b] : edges) {
        cin>>a>>b;
        deg[a]++;
        deg[b]++;
    }
    
    ll ans = 0;
    for(auto [a,b] : edges) if(min(deg[a], deg[b]) >= 3) {
        ans += ((deg[a] - 1) * (deg[a] - 2) / 2) * ((deg[b] - 1) * (deg[b] - 2) / 2);
    }
    cout<<ans;
    
}
```
