```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    cin.tie(0)->sync_with_stdio(0);
    int N,M;
    cin>>N>>M;
    bool v[501][501]{};
    for(int i=0,a,b;i<M;i++) {
        cin>>a>>b;
        v[a][b] = v[b][a] = 1;
    }
    int Q;
    for(cin>>Q;Q--;) {
        int a,b,c;
        cin>>a>>b>>c;
        int d = a&1;
        v[b][c] = v[c][b] = d;
        
        int ans[501]{};
        for(int i=1;i<=N;i++) ans[i] = -1;
        queue<pair<int,int>> q;
        q.emplace(1,0);
        bitset<501> vis;
        vis[1] = 1;
        while(!q.empty()) {
            auto [n,t] = q.front(); q.pop();
            ans[n] = t;
            for(int i=1;i<=N;i++) if(v[n][i] && !vis[i]) {
                vis[i] = 1;
                q.emplace(i,t+1);
            }
        }
        for(int i=1;i<=N;i++) cout<<ans[i]<<' ';
        cout<<'\n';
    }
}
```
