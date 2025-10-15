```cpp
#include <bits/stdc++.h>
using namespace std;

int T, N, a, d[5001]{};

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    for(int i=2;i<=5000;i++) {
        bitset<5000> v;
        for(int j=0;j<=i-j-2;j++) v[d[j]^d[i-j-2]]=1;
        while(v[d[i]]) d[i]++;
    }

    for(cin>>T;T--;cout<<(d[a] ? "First\n" : "Second\n")) cin>>a;

}
```
