```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

ll N, M, R, d[101][101]{}, e[101]{}, v[100001]{}, s[100001]{};

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N>>M>>R;
    for(int i=1;i<=M;i++) for(int j=1;j<=M;j++) cin>>d[i][j];
    for(int i=1;i<=M;i++) for(int j=1;j<=M;j++) for(int k=1;k<=M;k++) d[j][k] = min(d[j][k], d[j][i] + d[i][k]);

    for(int i=1;i<=M;i++) cin>>e[i];

    for(int p=1,i=1;i<=N;i++) {
        cin>>v[i];
        s[i] = s[i-1] + d[p][v[i]];
        p = v[i];
    }

    ll mn = 1e18, ans = 1e18;
    for(int i=1;i<=N;i++) {
        int l = i, r = N, m = (l+r)>>1;
        ll f = s[i] + e[v[i]];
        while(l<r) {
            ll z = 0;
            if(m < N) z += d[v[i]][v[m+1]] + s[N]-s[m+1];
            if(f+z <= R) r = m;
            else l = m+1;
            m = (l+r)>>1;
        }
        ll cnt = m-i, res = f;
        if(m < N) res += d[v[i]][v[m+1]] + s[N]-s[m+1];
        if(res > R) continue;
        if(cnt < mn || (cnt == mn && res < ans)) mn = cnt, ans = res;
    }
    if(mn == 1e18) cout<<-1;
    else cout<<mn<<' '<<ans;

}
```
