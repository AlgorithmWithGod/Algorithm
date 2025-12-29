```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M, K, a[10001]{}, r[10001]{};
int f(int x) { return x==r[x] ? x : r[x]=f(r[x]); }

int main() {
    cin.tie(0)->sync_with_stdio(0);

    cin>>N>>M>>K;
    iota(r, r+N+1, 0);
    for(int i=1;i<=N;i++) cin>>a[i];
    for(int u,v;M--;) {
        cin>>u>>v;
        int x = f(u), y = f(v);
        if(x == y) continue;
        a[y] = min(a[x], a[y]);
        r[x] = y;
    }

    bitset<10001> vis;
    int tot = 0;
    for(int i=1;i<=N;i++) if(!vis[f(i)]) {
        vis[f(i)].flip();
        tot += a[f(i)];
        if(tot > K) return cout<<"Oh no", 0;
    }
    cout<<tot;

}
```
