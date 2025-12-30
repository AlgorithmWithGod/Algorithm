```cpp
#include <bits/stdc++.h>
using namespace std;

const int INF = 1e9 + 7;

int N, I, G;
int dp[202][202]{};

int main() {
    cin.tie(0)->sync_with_stdio(0);

    cin>>N>>I>>G;
    for(int i=0;i<=201;i++) for(int j=0;j<=201;j++) dp[i][j] = INF;
    dp[0][0] = 0;

    for(int i,g;N--;) {
        cin>>i>>g;
        int ndp[202][202]{};
        for(int a=0;a<=201;a++) for(int b=0;b<=201;b++) ndp[a][b] = INF;
        for(int a=0;a<=200;a++) for(int b=0;b<=200;b++) if(dp[a][b] != INF) {
            int A = min(201, a+i), B = min(201, b+g);
            ndp[A][B] = min(ndp[A][B], dp[a][b] + 1);
        }
        for(int a=0;a<=200;a++) {
            if(dp[201][a] != INF) {
                int A = min(201, a+g);
                ndp[201][A] = min(ndp[201][A], dp[201][a] + 1);
            }
            if(dp[a][201] != INF) {
                int A = min(201, a+i);
                ndp[A][201] = min(ndp[A][201], dp[a][201] + 1);
            }
        }
        for(int a=0;a<=201;a++) for(int b=0;b<=201;b++) dp[a][b] = min(dp[a][b], ndp[a][b]);
    }

    int ans = INF;
    for(int i=I;i<=201;i++) for(int j=G;j<=201;j++) ans = min(ans, dp[i][j]);
    cout<<(ans == INF ? -1 : ans);

}
```
