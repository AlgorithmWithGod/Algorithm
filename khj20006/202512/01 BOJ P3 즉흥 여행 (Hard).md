```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M;
vector<vector<int>> g(200001), r(200001), v(200001);
bitset<200001> vis;
stack<int> st;
int num[200001]{}, deg[200001]{}, dp[200001]{};

void dfs1(int n) {
    for(int i:g[n]) if(!vis[i]) {
        vis[i] = 1;
        dfs1(i);
    }
    st.push(n);
}

void dfs2(int n, int k) {
    num[n] = k;
    for(int i:r[n]) if(!vis[i]) {
        vis[i] = 1;
        dfs2(i, k);
    }
}

int main(){
	cin.tie(0)->sync_with_stdio(0);

	cin>>N>>M;
    for(int a,b;M--;) {
        cin>>a>>b;
        g[a].push_back(b);
        r[b].push_back(a);
    }

    for(int i=1;i<=N;i++) if(!vis[i]) {
        vis[i] = 1;
        dfs1(i);
    }

    int cnt = 0;
    vis.reset();
    while(!st.empty()) {
        int n = st.top(); st.pop();
        if(vis[n]) continue;
        vis[n] = 1;
        dfs2(n, ++cnt);
    }

    for(int i=1;i<=N;i++) for(int j:g[i]) if(num[i] != num[j]) {
        deg[num[i]]++;
        v[num[j]].push_back(num[i]);
    }

    queue<int> q;
    for(int i=1;i<=cnt;i++) if(!deg[i]) {
        q.push(i);
        dp[i] = 1;
    }

    while(!q.empty()) {
        int n = q.front(); q.pop();
        for(int i:v[n]) {
            if(!--deg[i]) q.push(i);
            dp[i] = max(dp[i], dp[n] + 1);
        }
    }

    vector<int> ans;
    for(int i=1;i<=N;i++) if(dp[num[i]] == cnt) ans.push_back(i);

    cout<<ans.size()<<'\n';
    for(int i:ans) cout<<i<<' ';

}
```
