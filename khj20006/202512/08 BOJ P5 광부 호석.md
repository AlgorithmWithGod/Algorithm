```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int N, C;
vector<tuple<int, int, int>> arr;
priority_queue<pair<int, int>> q;

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N>>C;
    arr.resize(N);
    for(auto &[x,y,v] : arr) cin>>x>>y>>v;
    sort(arr.begin(), arr.end());
    
    ll ans = 0, cur = 0;
    for(int i=0;i<arr.size();) {
        int x = get<0>(arr[i]);
        while(i<arr.size() && get<0>(arr[i]) == x) {
            cur += get<2>(arr[i]);
            q.emplace(get<1>(arr[i]), get<2>(arr[i]));
            i++;
        }
        while(q.size() > C) {
            auto [y, v] = q.top(); q.pop();
            cur -= v;
            while(!q.empty() && q.top().first == y) {
                cur -= q.top().second;
                q.pop();
            }
        }
        ans = max(ans, cur);
    }
    
    cout<<ans;
    
}
```
