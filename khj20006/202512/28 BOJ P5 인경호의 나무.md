```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

const ll MOD = 1e9 + 7;

int N, M;
int a[1001]{}, l[1001]{}, r[1001]{};
ll c[2001][1001]{};

vector<int> res;

void inorder(int n) {
    if(l[n] != -1) inorder(l[n]);
    res.push_back(a[n]);
    if(r[n] != -1) inorder(r[n]);
}

int main() {
    cin.tie(0)->sync_with_stdio(0);

    for(int k=1;k<=2000;k++) {
        c[k][1] = k;
        for(int i=2;i<=min(k,1000);i++) c[k][i] = (c[k-1][i-1] + c[k-1][i]) % MOD;
    }

    cin>>N>>M;
    for(int i=1;i<=N;i++) cin>>a[i]>>l[i]>>r[i];

    inorder(1);
    res.push_back(M+1);
    ll ans = 1, prev = 0;
    for(int i=0;i<res.size();i++) {
        if(res[i] == -1) {
            int cnt = 0;
            while(i<res.size() && res[i] == -1) i++, cnt++;
            if(res[i] <= prev) return cout<<0,0;
            if(cnt > res[i] - prev - 1) return cout<<0,0;
            ans = (ans * c[res[i]-prev-1][cnt]) % MOD;
        }
        prev = res[i];
    }
    cout<<ans;

}
```
