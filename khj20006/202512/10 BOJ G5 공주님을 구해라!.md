```cpp
#include <bits/stdc++.h>
using namespace std;

const int dx[4] = {1,0,-1,0};
const int dy[4] = {0,1,0,-1};

int N, M, T;
int arr[100][100]{};
queue<tuple<int, int, int>> q;
bool vis[100][100]{};
int paint = 1234567;

int main() {
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N>>M>>T;
    for(int i=0;i<N;i++) for(int j=0;j<M;j++) cin>>arr[i][j];
    
    q.emplace(0,0,0);
    vis[0][0] = 1;
    while(!q.empty()) {
        auto [x,y,t] = q.front(); q.pop();
        if(arr[x][y] == 2) {
            paint = t + abs(N-x-1) + abs(M-y-1);
        }
        if(x == N-1 && y == M-1) {
            int val = min(paint, t);
            if(val > T) cout<<"Fail";
            else cout<<val;
            return 0;
        }
        for(int i=0;i<4;i++) {
            int xx = x+dx[i], yy = y+dy[i];
            if(xx<0 || xx>=N || yy<0 || yy>=M || vis[xx][yy] || arr[xx][yy] == 1) continue;
            vis[xx][yy] = 1;
            q.emplace(xx,yy,t+1);
        }
    }
    if(paint > T) cout<<"Fail";
    else cout<<paint;
    
}
```
