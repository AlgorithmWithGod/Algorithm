```cpp
#include <bits/stdc++.h>
using namespace std;

const int dx[3] = {1,0,-1};
const int dy[3] = {0,1,-1};

int N;
int arr[1000][1000]{};
bool vis[1000][1000]{};

bool oob(int x, int y) {
    return x<0 || x>=N || y<0 || y>x;
}

void go(int x, int y, int value, int dir) {
    if(value > N*(N+1)/2) return;
    arr[x][y] = value;
    vis[x][y] = true;
    int xx = x + dx[dir];
    int yy = y + dy[dir];
    if(oob(xx,yy) || vis[xx][yy]) {
        dir = (dir + 1) % 3;
        xx = x + dx[dir];
        yy = y + dy[dir];
    }
    go(xx,yy,value+1,dir);
}

vector<int> solution(int n) {
    N = n;
    go(0,0,1,0);
    vector<int> answer;
    for(int i=0;i<N;i++) for(int j=0;j<=i;j++) answer.push_back(arr[i][j]);
    return answer;
}
```
