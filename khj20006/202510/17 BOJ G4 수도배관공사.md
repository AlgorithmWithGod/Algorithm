```cpp
#include <bits/stdc++.h>
using namespace std;

const int INF = 1e9+7;

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    int D, P;
    cin>>D>>P;
    vector<int> dp(100001, INF);
    for(int l, c;P--;) {
        cin>>l>>c;
        for(int j=100000;j>l;j--) if(dp[j-l] != INF) {
            if(dp[j] == INF) dp[j] = min(dp[j-l], c);
            else dp[j] = max(dp[j], min(dp[j-l], c));
        }
        if(dp[l] == INF) dp[l] = c;
        else dp[l] = max(dp[l], c);
    }
    
    cout<<dp[D];
}
```
