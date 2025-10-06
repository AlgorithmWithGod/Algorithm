```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int T, N;
vector<pair<ll, ll>> v;
vector<ll> L, R;

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    for(cin>>T;T--;) {
        cin>>N;
        v = vector<pair<ll, ll>>(N);
        for(auto &[a,b]:v) cin>>a>>b;
        if(N == 1) {
            cout<<"0\n";
            continue;
        }

        sort(v.begin(), v.end());
        
        L = vector<ll>(N);
        ll mx = v[0].second, mn = v[0].second;
        for(int i=0;i<N;i++) {
            mx = max(mx, v[i].second);
            mn = min(mn, v[i].second);
            L[i] = (v[i].first-v[0].first) * (mx-mn);
        }
        
        R = vector<ll>(N);
        mx = v[N-1].second, mn = v[N-1].second;
        for(int i=N-1;i>=0;i--) {
            mx = max(mx, v[i].second);
            mn = min(mn, v[i].second);
            R[i] = (v[N-1].first-v[i].first) * (mx-mn);
        }

        ll ans = 1e18;
        for(int i=1;i<N;i++) ans = min(ans, max(L[i-1], R[i]));
        
        sort(v.begin(), v.end(), [](auto a, auto b) -> bool {
            return a.second == b.second ? a.first < b.first : a.second < b.second;
        });
        
        L = vector<ll>(N);
        mx = v[0].first, mn = v[0].first;
        for(int i=0;i<N;i++) {
            mx = max(mx, v[i].first);
            mn = min(mn, v[i].first);
            L[i] = (v[i].second-v[0].second) * (mx-mn);
        }

        R = vector<ll>(N);
        mx = v[N-1].first, mn = v[N-1].first;
        for(int i=N-1;i>=0;i--) {
            mx = max(mx, v[i].first);
            mn = min(mn, v[i].first);
            R[i] = (v[N-1].second-v[i].second) * (mx-mn);
        }

        for(int i=1;i<N;i++) ans = min(ans, max(L[i-1], R[i]));
        cout<<ans<<'\n';
    }

}
```
