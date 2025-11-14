```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

const ll INF = 1e18;
int N, S, E;
map<int, vector<tuple<int, int, ll>>> mp[8]{};
vector<vector<pair<int, ll>>> v(100001);
vector<ll> dist(100001, INF);
int par[100001]{};

int main() {
    cin.tie(0)->sync_with_stdio(0);

    cin>>N>>S>>E;
    for(int i=1;i<=N;i++) {
        int x,y,c;
        string d;
        cin>>x>>y>>c>>d;

        int dir = -1;
        if(d == "N") dir = 0;
        if(d == "NE") dir = 1;
        if(d == "E") dir = 2;
        if(d == "SE") dir = 3;
        if(d == "S") dir = 4;
        if(d == "SW") dir = 5;
        if(d == "W") dir = 6;
        if(d == "NW") dir = 7;

        int cost = 0;
        for(int j=dir;j<dir+8;j++) {
            int k = j%8;
            if(k == 0) {
                mp[k][x].emplace_back(y,i,cost);
            }
            else if(k == 1) {
                mp[k][y-x].emplace_back(x,i,cost);
            }
            else if(k == 2) {
                mp[k][y].emplace_back(x,i,cost);
            }
            else if(k == 3) {
                mp[k][y+x].emplace_back(x,i,cost);
            }
            else if(k == 4) {
                mp[k][x].emplace_back(y,i,cost);
            }
            else if(k == 5) {
                mp[k][y-x].emplace_back(x,i,cost);
            }
            else if(k == 6) {
                mp[k][y].emplace_back(x,i,cost);
            }
            else {
                mp[k][y+x].emplace_back(x,i,cost);
            }
            cost += c;
        }

    }

    for(int i=0;i<8;i++) {
        for(auto [a,b] : mp[i]) {
            if(i<4) sort(b.begin(), b.end());
            else sort(b.begin(), b.end(), greater<>());

            for(int j=1;j<b.size();j++) {
                auto [p,n1,c1] = b[j-1];
                auto [q,n2,c2] = b[j];
                v[n1].emplace_back(n2,c1);
            }
        }
    }

    dist[S] = 0;
    priority_queue<pair<ll, int>, vector<pair<ll, int>>, greater<>> q;
    q.emplace(0,S);
    while(!q.empty()) {
        auto [d,n] = q.top(); q.pop();
        if(d > dist[n]) continue;
        if(n == E) {
            cout<<d<<'\n';
            stack<int> st;
            while(n) {
                st.push(n);
                n = par[n];
            }
            while(!st.empty()) {
                cout<<st.top()<<' ';
                st.pop();
            }
            return 0;
        }
        for(auto [i,c]:v[n]) if(dist[i] > d+c) {
            dist[i] = d+c;
            par[i] = n;
            q.emplace(dist[i], i);
        }
    }
    cout<<-1;

}
```
