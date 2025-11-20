```cpp
#include <bits/stdc++.h>
using namespace std;

int D, L;
vector<vector<int>> v(5001), r(5001);

bitset<5001> vis;
int cnt = 0, ans = 0;
stack<int> st;

void dfs1(int n) {
    for(int i:v[n]) if(!vis[i]) {
        vis[i] = 1;
        dfs1(i);
    }
    st.push(n);
}

void dfs2(int n) {
    cnt++;
    for(int i:r[n]) if(!vis[i]) {
        vis[i] = 1;
        dfs2(i);
    }
}

int main(){
    cin.tie(0)->sync_with_stdio(0);

    for(cin>>D>>L;L--;) {
        int a,b;
        cin>>a>>b;
        v[a].push_back(b);
        r[b].push_back(a);
    }

    for(int i=1;i<=D;i++) if(!vis[i]) {
        vis[i] = 1;
        dfs1(i);
    }
    vis.reset();
    while(!st.empty()) {
        int n = st.top(); st.pop();
        if(vis[n]) continue;
        cnt = 0;
        vis[n] = 1;
        dfs2(n);
        ans = max(ans, cnt);
    }

    cout<<ans;

}
```
