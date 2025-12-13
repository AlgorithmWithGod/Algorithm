```cpp
#include <bits/stdc++.h>
using namespace std;

int N;
vector<int> v;

int main() {
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N;
    for(int a;N--;) {
        cin>>a;
        int idx = lower_bound(v.begin(), v.end()) - v.begin();
        if(idx == v.size()) v.push_back(a);
        else v[idx] = a;
    }
    cout<<v.size();
    
}
```
