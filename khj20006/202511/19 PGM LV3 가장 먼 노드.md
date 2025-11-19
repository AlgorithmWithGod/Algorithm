```cpp
#include <bits/stdc++.h>
using namespace std;

int solution(int n, vector<vector<int>> edge) {
    const int INF = 123456;
    
    vector<vector<int>> graph(n+1);
    for(auto e : edge) {
        int a = e[0], b = e[1];
        graph[a].push_back(b);
        graph[b].push_back(a);
    }
    
    queue<pair<int, int>> q;
    vector<int> dist(n+1, INF);
    q.emplace(1,0);
    dist[1] = 0;
    int mx = 0;
    while(!q.empty()) {
        auto [n,d] = q.front(); q.pop();
        mx = max(mx, d);
        for(int i:graph[n]) if(dist[i] == INF) {
            dist[i] = d+1;
            q.emplace(i, dist[i]);
        }
    }
    
    int ans = 0;
    for(int i=1;i<=n;i++) if(dist[i] == mx) ans++;
    
    return ans;
}
```