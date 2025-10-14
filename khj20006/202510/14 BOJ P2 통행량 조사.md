```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M, cycCount = 0, E, R, r[200001]{}, ans[200001]{}, dep[200001]{}, s[200001]{}, par[200001][18]{}, cyc[200001][18]{};
vector<vector<pair<int, int>>> v(200001);

int f(int x) {return x==r[x] ? x : r[x]=f(r[x]);}

int fillCycle(int n, int p, int t) {
    if(n == t) return cyc[n][0] = 1;
    for(auto [i,_]:v[n]) if(i != p) {
        cyc[n][0] |= fillCycle(i,n,t);
    }
    return cyc[n][0];
}

void dfs(int n, int p, int d) {
    par[n][0] = p, dep[n] = d;
    for(auto [i,_]:v[n]) if(i != p) dfs(i,n,d+1);
}

int cle(int n, int p) {
    for(auto [i,g]:v[n]) if(i != p) {
        s[n] += cle(i,n);
        if(cyc[i][0]) ans[g] += cycCount;
        ans[g] += s[i];
    }
    return s[n];
}

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N>>M;
    iota(r, r+N+1, 0);
    for(int i=0,a,b;i<N;i++) {
        cin>>a>>b;
        int x = f(a), y = f(b);
        if(x == y) {
            fillCycle(a,0,b);
            E = i;
            R = a;
        }
        else {
            v[a].emplace_back(b,i);
            v[b].emplace_back(a,i);
            r[x] = y;
        }
    }

    dfs(R,0,0);
    for(int k=1;k<18;k++) for(int i=1;i<=N;i++) {
        par[i][k] = par[par[i][k-1]][k-1];
        cyc[i][k] = cyc[i][k-1] + cyc[par[i][k-1]][k-1];
    }

    for(int x,y,c;M--;) {
        cin>>x>>y>>c;
        int a = x, b = y;
        int cycSum = 0, diff = abs(dep[a]-dep[b]);
        for(int k=0;k<18;k++) if(diff & (1<<k)) {
            if(dep[a] < dep[b]) swap(a,b);
            cycSum += cyc[a][k];
            a = par[a][k];
        }
        for(int k=17;k>=0;k--) if(par[a][k] != par[b][k]) {
            cycSum += cyc[a][k] + cyc[b][k];
            a = par[a][k], b = par[b][k];
        }
        if(a != b) {
            cycSum += cyc[a][0] + cyc[b][0];
            a = par[a][0], b = par[b][0];
        }
        int lca = a;
        cycSum += cyc[lca][0];

        s[x] += c;
        s[y] += c;
        if(cycSum > 1) {
            cycCount += c;
            for(int k=17;k>=0;k--) {
                if(!cyc[x][k]) x = par[x][k];
                if(!cyc[y][k]) y = par[y][k];
            }
            s[x] -= c;
            s[y] -= c;
        }
        else {
            s[lca] -= 2*c;
        }
        
    }
    cle(R,0);
    ans[E] += cycCount;
    for(int i=0;i<N;i++) cout<<ans[i]<<'\n';

}
```
