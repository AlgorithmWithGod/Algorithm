```cpp

#include <iostream>
#include <vector>
using namespace std;

int dx[4] = {1,0,-1,0};
int dy[4] = {0,1,0,-1};
char A[5][9]{};
vector<pair<int,int>> P;
bool vis[8]{};
int cnt, mv;

bool ok(int x, int y) {return 0<=x&&x<5 && 0<=y&&y<9;}
bool isNumber(int x, int y) {return '0'<=A[x][y] && A[x][y]<='9';}

void bck(int c, int m){
    if(c < cnt || (c == cnt && m < mv)) cnt = c, mv = m;
    if(!c) return;
    for(int i=0;i<P.size();i++) if(!vis[i]){
        auto &[x,y] = P[i];
        int px = x, py = y;
        for(int k=0;k<4;k++){
            int nx = x+dx[k], ny = y+dy[k];
            if(!ok(nx,ny) || !isNumber(nx,ny)) continue;
            int nnx = nx+dx[k], nny = ny+dy[k];
            if(!ok(nnx,nny) || A[nnx][nny] != '.') continue;

            int rem = A[nx][ny] - '0';
            vis[rem] = 1;
            A[nnx][nny] = A[x][y];
            A[nx][ny] = '.';
            A[x][y] = '.';
            x = nnx, y = nny;
            bck(c-1, m+1);
            x = px, y = py;
            vis[rem] = 0;
            A[x][y] = A[nnx][nny];
            A[nx][ny] = '0' + rem;
            A[nnx][nny] = '.';
        }
    }
}

int main(){
    cin.tie(0)->sync_with_stdio(0);

    int T;
    for(cin>>T;T--;){
        cnt = 0, mv = 0;
        P = vector<pair<int, int>>();
        for(int i=0;i<8;i++) vis[i]=0;
        for(int i=0;i<5;i++) for(int j=0;j<9;j++) {
            cin>>A[i][j];
            if(A[i][j] == 'o') {
                P.emplace_back(i,j), A[i][j] = '0' + (cnt);
                cnt++;
            }
        }
        bck(cnt, 0);
        cout<<cnt<<' '<<mv<<'\n';
    }

}

```
