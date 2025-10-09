```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M, W, F, t[50000]{}, d[50000][4]{};
vector<vector<pair<int, int>>> v(50000);

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N>>M>>W>>F;
    for(int i=1,a;i<=W;i++) {
        cin>>a;
        t[a] |= 1;
    }
    for(int i=1,a;i<=F;i++) {
        cin>>a;
        t[a] |= 2;
    }

    for(int a,b,c;M--;) {
        cin>>a>>b>>c;
        v[a].emplace_back(b,c);
        v[b].emplace_back(a,c);
    }

    for(int i=0;i<N;i++) for(int j=0;j<4;j++) d[i][j] = 1e9;
    d[0][t[0]] = 0;
    priority_queue<tuple<int, int, int>, vector<tuple<int, int, int>>, greater<>> q;
    q.emplace(0,0,t[0]);
    while(!q.empty()) {
        auto [s, n, k] = q.top(); q.pop();
        if(s > d[n][k]) continue;
        for(auto [i,c]:v[n]) {
            int r = k | t[i];
            if(d[i][r] > s+c) {
                d[i][r] = s+c;
                q.emplace(s+c,i,r);
            }
        }
    }
    cout<<d[0][3];

}
```