```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M, R;
vector<vector<int>> v(100001);

pair<int, int> f(int n, int p, int t) {
    int d = t, c = 0, l = 0;
    for(int i:v[n]) if(i != p) {
        auto [dd, cc] = f(i, n, t);
        d = min(d, dd+1);
        c += cc;
        l++;
    }
    if(!l) return {0,1};
    if(d == t && n != R) c++, d = 0;
    return {d,c};
}

int main() {
    cin.tie(0)->sync_with_stdio(0);

    cin>>N>>M>>R;
    for(int i=1,a,b;i<N;i++) {
        cin>>a>>b;
        v[a].push_back(b);
        v[b].push_back(a);
    }

    int s = 1, e = N, m = (s+e)>>1;
    while(s<e) {
        if(f(R, 0, m).second > M) s = m+1;
        else e = m;
        m = (s+e)>>1;
    }
    cout<<(m == N ? -1 : m);

}
```
