```cpp
#include <bits/stdc++.h>
using namespace std;

int N;
vector<vector<int>> v(200001);
int dep[200001]{};
int par[200001][18]{}, dist[200001][18]{};

void dfs(int n, int p, int d) {
    dep[n] = d, par[n][0] = p;
    for(int i:v[n]) if(i != p) {
        dfs(i,n,d+1);
        dist[i][0] = 1;
    }
}

int main() {
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N;
    for(int i=1,a,b;i<N;i++){
        cin>>a>>b;
        v[a].push_back(b);
        v[b].push_back(a);
    }
    
    dfs(1,0,0);
    for(int k=1;k<18;k++) for(int i=1;i<=N;i++) {
        par[i][k] = par[par[i][k-1]][k-1];
        dist[i][k] = dist[i][k-1] + dist[par[i][k-1]][k-1];
    }
    
    long long ans = 0;
    for(int i=1;i<=N;i++) for(int j=i*2;j<=N;j+=i) {
        int a = i, b = j, diff = abs(dep[a] - dep[b]);
        
        for(int k=0;k<18;k++) if(diff & (1<<k)) {
            if(dep[a] > dep[b]) swap(a,b);
            ans += dist[b][k];
            b = par[b][k];
        }
        
        for(int k=17;k>=0;k--) if(par[a][k] != par[b][k]) {
            ans += dist[a][k] + dist[b][k];
            a = par[a][k];
            b = par[b][k];
        }
        if(a != b) {
            ans += 2;
        }
        ans++;
    }
    
    cout<<ans;
    
}
```
