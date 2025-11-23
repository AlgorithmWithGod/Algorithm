```cpp
#include <bits/stdc++.h>
using namespace std;

const int dx[4] = {1,0,-1,0};
const int dy[4] = {0,1,0,-1};

int N, Q;
char arr[1001][1001]{};
int srr[1001][1001]{};
int cost[1000001]{}, root[1000001]{}, depth[1000001]{}, par[1000001][20]{}, val[1000001][20]{};

vector<tuple<int, int, int>> edges;
vector<vector<int>> v(1000001);

int find(int x) { return x == root[x] ? x : root[x]=find(root[x]); }

int sum(int x, int y, int xx, int yy) {
    return srr[xx][yy] - srr[xx][y-1] - srr[x-1][yy] + srr[x-1][y-1];
}

void dfs(int n, int p, int d) {
    par[n][0] = p, depth[n] = d;
    for(int i:v[n]) if(i != p) {
        dfs(i,n,d+1);
        val[i][0] = cost[n];
    }
}

int main(){
    cin.tie(0)->sync_with_stdio(0);

    cin>>N;
    for(int i=1;i<=N;i++) for(int j=1;j<=N;j++) {
        cin>>arr[i][j];
        srr[i][j] = (arr[i][j] == '#' ? 1 : 0) + srr[i-1][j] + srr[i][j-1] - srr[i-1][j-1];
    }

    for(int i=1;i<=N;i++) for(int j=1;j<=N;j++) if(arr[i][j] != '#') {
        int s = 0;
        int e = min({abs(i-1), abs(N-i), abs(j-1), abs(N-j)});
        int m = (s+e+1)>>1;
        while(s<e) {
            if(sum(i-m,j-m,i+m,j+m)) e = m-1;
            else s = m;
            m = (s+e+1)>>1;
        }
        cost[(i-1)*N+j] = 2*m+1;
    }

    for(int i=0;i<N;i++) for(int j=0;j<N;j++) {
        for(int k=0;k<4;k++) {
            int x = i+dx[k], y = j+dy[k];
            if(x<0 || x>=N || y<0 || y>=N) continue;
            int c = min(cost[i*N+j+1], cost[x*N+y+1]);
            edges.emplace_back(c, i*N+j+1, x*N+y+1);
        }
    }

    sort(edges.begin(), edges.end(), greater<>());
    iota(root, root+N*N+1, 0);
    for(auto [c,a,b] : edges) {
        int x = find(a), y = find(b);
        if(x == y) continue;
        root[x] = y;
        v[a].push_back(b);
        v[b].push_back(a);
    }

    dfs(1,0,0);
    for(int k=1;k<20;k++) for(int i=1;i<=N*N;i++) {
        par[i][k] = par[par[i][k-1]][k-1];
        val[i][k] = min(val[i][k-1], val[par[i][k-1]][k-1]);
    }

    for(cin>>Q;Q--;) {
        int a,b,c,d;
        cin>>a>>b>>c>>d;
        int aa = (a-1)*N+b, bb = (c-1)*N+d;
        
        int res = min(cost[aa], cost[bb]);
        int diff = abs(depth[aa] - depth[bb]);
        for(int k=0;k<20;k++) if(diff & (1<<k)) {
            if(depth[aa] > depth[bb]) {
                res = min(res, val[aa][k]);
                aa = par[aa][k];
            }
            else {
                res = min(res, val[bb][k]);
                bb = par[bb][k];
            }
        }

        for(int k=19;k>=0;k--) if(par[aa][k] != par[bb][k]) {
            res = min({res, val[aa][k], val[bb][k]});
            aa = par[aa][k];
            bb = par[bb][k];
        }
        if(aa != bb) {
            res = min({res, val[aa][0], val[bb][0]});
        }

        cout<<res<<'\n';
    }

}
```
