```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    cin.tie(0)->sync_with_stdio(0);
    
    int N, M, a[100001]{}, b[100001]{};
    cin>>N>>M;
    for(int i=1;i<=N;i++) cin>>a[i];
    for(int x,y,z;M--;) {
        cin>>x>>y>>z;
        b[x] += z;
        b[y+1] -= z;
    }
    int s = 0;
    for(int i=1;i<=N;i++) {
        s += b[i];
        cout<<a[i]+s<<' ';
    }
    
}
```
