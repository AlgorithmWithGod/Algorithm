```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int N;
vector<vector<int>> v;
vector<ll> a, d, s, u;

void dfs1(int n, int p) {
    s[n] = 1;
    for(int i:v[n]) if(i != p) {
        dfs1(i,n);
        s[n] += s[i];
        d[n] += d[i] + (a[n]^a[i]) * s[i];
    }
}

void dfs2(int n, int p) {
    if(n != 1) u[n] = u[p] + d[p] - d[n] + (a[n]^a[p]) * (N - 2 * s[n]);
    for(int i:v[n]) if(i != p) dfs2(i,n);
}

int main() {
    cin.tie(0)->sync_with_stdio(0);
    
    int T;
    for(cin>>T;T--;) {
        cin>>N;
        a = vector<ll>(N+1);
        d = vector<ll>(N+1);
        s = vector<ll>(N+1);
        u = vector<ll>(N+1);
        v = vector<vector<int>>(N+1);
        for(int i=1;i<=N;i++) cin>>a[i];
        for(int i=1,p,q;i<N;i++) {
            cin>>p>>q;
            v[p].push_back(q);
            v[q].push_back(p);
        }
        dfs1(1,0);
        dfs2(1,0);
        for(int i=1;i<=N;i++) cout<<d[i]+u[i]<<' ';
        cout<<'\n';
    }

}
```
