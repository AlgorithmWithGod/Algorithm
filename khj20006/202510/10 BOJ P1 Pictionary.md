```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M, Q, r[100001]{}, dep[100001]{}, par[100001][17]{}, mx[100001][17]{};
vector<vector<pair<int, int>>> v(100001);

int f(int x) {return x==r[x] ? x : r[x]=f(r[x]);}

void dfs(int n, int p, int d) {
    par[n][0] = p, dep[n] = d;
    for(auto [i,c]:v[n]) if(i != p) {
        mx[i][0] = c;
        dfs(i,n,d+1);
    }
}

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N>>M>>Q;
    iota(r, r+N+1, 0);
    for(int g=M,i=1;g>0;g--,i++) {
        for(int j=g;j+g<=N;j+=g) {
            int x = f(j), y = f(j+g);
            if(x == y) continue;
            r[x] = y;
            v[j].emplace_back(j+g,i);
            v[j+g].emplace_back(j,i);
        }
    }

    dfs(1,0,0);
    for(int k=1;k<17;k++) for(int i=1;i<=N;i++) {
        par[i][k] = par[par[i][k-1]][k-1];
        mx[i][k] = max(mx[i][k-1], mx[par[i][k-1]][k-1]);
    }

    for(int a,b;Q--;) {
        cin>>a>>b;
        int ans = 1, diff = abs(dep[a] - dep[b]);
        for(int k=0;k<17;k++) if(diff & (1<<k)) {
            if(dep[a] > dep[b]) ans = max(ans, mx[a][k]), a = par[a][k];
            else ans = max(ans, mx[b][k]), b = par[b][k];
        }
        for(int k=16;k>=0;k--) if(par[a][k] != par[b][k]) {
            ans = max({ans, mx[a][k], mx[b][k]});
            a = par[a][k], b = par[b][k];
        }
        if(a != b) ans = max({ans, mx[a][0], mx[b][0]});
        cout<<ans<<'\n';
    }

}
```
