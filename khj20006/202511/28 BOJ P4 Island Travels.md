```cpp
#include <bits/stdc++.h>
using namespace std;

const int dx[4] = {1,0,-1,0};
const int dy[4] = {0,1,0,-1};
const int INF = 1e9 + 7;

int N, W, H;
char arr[50][50]{};
int num[50][50]{};
bool vis[50][50]{};
int cost[15][15]{};
int dp[15][1<<15]{};
vector<vector<pair<int, int>>> islands;

int get(int n, int k) {
    if(dp[n][k] != INF) return dp[n][k];
    int &ret = dp[n][k];
    int p = k ^ (1<<n);
    for(int i=0;i<N;i++) if((1<<i) & p) ret = min(ret, get(i,p) + cost[i][n]);
    return ret;
}

int main(){
    cin.tie(0)->sync_with_stdio(0);

    cin>>W>>H;
    for(int i=0;i<W;i++) for(int j=0;j<H;j++) cin>>arr[i][j], num[i][j] = -1;

    for(int i=0;i<W;i++) for(int j=0;j<H;j++) if(arr[i][j] == 'X' && !vis[i][j]) {
        queue<pair<int, int>> q;
        q.emplace(i,j);
        vis[i][j] = 1;
        vector<pair<int, int>> grounds;
        while(!q.empty()) {
            auto [x,y] = q.front(); q.pop();
            num[x][y] = islands.size();
            grounds.emplace_back(x,y);
            for(int k=0;k<4;k++) {
                int xx = x+dx[k], yy = y+dy[k];
                if(xx<0 || xx>=W || yy<0 || yy>=H || arr[xx][yy] != 'X' || vis[xx][yy]) continue;
                vis[xx][yy] = 1;
                q.emplace(xx,yy);
            }
        }
        islands.push_back(grounds);
    }

    N = islands.size();
    if(N == 1) return cout<<0, 0;
    for(int i=0;i<N;i++) for(int j=0;j<N;j++) cost[i][j] = INF;

    for(int i=0;i<N;i++) {
        for(int i=0;i<W;i++) for(int j=0;j<H;j++) vis[i][j] = 0;

        queue<tuple<int, int, int>> q;
        for(auto [x,y] : islands[i]) {
            q.emplace(x,y,0);
            vis[x][y] = 1;
        }
        while(!q.empty()) {
            auto [x,y,d] = q.front(); q.pop();
            for(int k=0;k<4;k++) {
                int xx = x+dx[k], yy = y+dy[k];
                if(xx<0 || xx>=W || yy<0 || yy>=H || arr[xx][yy] == '.' || vis[xx][yy]) continue;
                if(arr[xx][yy] == 'X') {
                    if(num[xx][yy] == num[x][y]) continue;
                    int a = num[xx][yy];
                    cost[a][i] = min(cost[a][i], d);
                    cost[i][a] = min(cost[i][a], d);
                }
                else {
                    q.emplace(xx,yy,d+1);
                    vis[xx][yy] = 1;
                }
            }
        }
    }

    for(int i=0;i<N;i++) for(int j=0;j<N;j++) for(int k=0;k<N;k++) cost[j][k] = min(cost[j][k], cost[j][i] + cost[i][k]);

    for(int i=0;i<N;i++) {
        for(int j=0;j<(1<<N);j++) dp[i][j] = INF;
        dp[i][1<<i] = 0;
    }

    int ans = INF;
    for(int i=0;i<N;i++) ans = min(ans, get(i,(1<<N)-1));
    cout<<ans;

}
```
