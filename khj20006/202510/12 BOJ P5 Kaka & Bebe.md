```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M;
vector<vector<tuple<int, int, int>>> v(1000);
vector<vector<int>> dist(1000, vector<int>(1001, -1));
priority_queue<tuple<int, int, int>, vector<tuple<int, int, int>>, greater<>> q;

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    for(cin>>N>>M;M--;) {
        int a,b,c,d;
        cin>>a>>b>>c>>d;
        v[a].emplace_back(b,c,d);
        v[b].emplace_back(a,c,d);
    }

    dist[0][0] = 0;
    q.emplace(0,0,0);
    while(!q.empty()) {
        auto [d,n,k] = q.top(); q.pop();
        if(d > dist[n][k]) continue;
        for(auto [i,x,y]:v[n]) if(k + x <= 1000) {
            if(dist[i][k+x] == -1 || dist[i][k+x] > d+y) {
                dist[i][k+x] = d+y;
                q.emplace(d+y, i, k+x);
            }
        }
    }

    int ans = -1;
    for(int i=0;i<=1000;i++) if(dist[N-1][i] != -1 && dist[N-1][i] <= 1000) {
        if(ans == -1) ans = dist[N-1][i] * i;
        else ans = min(ans, dist[N-1][i] * i);
    }
    cout<<ans;

}
```
