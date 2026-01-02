```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

const ll INF = 1e18;
const string S = "UOSPC";

int N;
string s;
ll arr[300000]{};

int main() {
    cin.tie(0)->sync_with_stdio(0);

    cin>>N>>s;
    for(int i=0;i<N;i++) cin>>arr[i];

    vector<ll> res(5, INF);
    for(int i=0;i<N;i++) {
        for(int j=0;j<5;j++) if(s[i] == S[j]) {
            if(!j) res[j] = min(res[j], arr[i]);
            else res[j] = min(res[j], res[j-1] + arr[i]);
        }
    }
    cout<<(res[4] == INF ? -1 : res[4]);

}
```
