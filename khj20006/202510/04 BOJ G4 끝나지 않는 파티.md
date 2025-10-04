```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M, c[501][501]{};

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N>>M;
    for(int i=1;i<=N;i++) for(int j=1;j<=N;j++) cin>>c[i][j];
    for(int i=1;i<=N;i++) for(int j=1;j<=N;j++) for(int k=1;k<=N;k++) c[j][k] = min(c[j][k], c[j][i] + c[i][k]);
    for(int a,b,C;M--;cout<<(c[a][b]<=C ? "Enjoy other party\n" : "Stay here\n")) cin>>a>>b>>C;

}
```
