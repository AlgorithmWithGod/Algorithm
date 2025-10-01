```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int N, Q, LIMIT;
ll w[262144]{}, l[524288]{}, r[524288]{}, x[524288]{};

void init(int n) {
    if(n >= LIMIT) return;
    init(n*2); init(n*2+1);
    l[n] = w[n] + max(l[n*2], r[n*2]);
    r[n] = w[n] + max(l[n*2+1], r[n*2+1]);
    x[n] = max({x[n*2], x[n*2+1], l[n] + r[n] - w[n]});
}

int main(){
    cin.tie(0)->sync_with_stdio(0);

    cin>>N;
    for(int i=1;i<=N;i++) cin>>w[i];
    LIMIT = N+1;
    init(1);
    cout<<x[1]<<'\n';
    for(cin>>Q;Q--;) {
        int i,d;
        cin>>i>>d;
        for(w[i]=d;i;i>>=1) {
            l[i] = w[i] + max(l[i*2], r[i*2]);
            r[i] = w[i] + max(l[i*2+1], r[i*2+1]);
            x[i] = max({x[i*2], x[i*2+1], l[i] + r[i] - w[i]});
        }
        cout<<x[1]<<'\n';
    }

}
```
