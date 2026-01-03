```cpp
#include <bits/stdc++.h>
using namespace std;

int N, X;
vector<int> primes;
bool ex[301][512]{};
bitset<512> base;

int main() {
    cin.tie(0)->sync_with_stdio(0);

    cin>>N>>X;
    for(int i=2;i*i<=X;i++) if(X%i == 0) {
        primes.push_back(i);
        while(X%i == 0) X /= i;
    }
    if(X != 1) primes.push_back(X);

    ex[0][(1<<primes.size())-1] = 1;
    for(int i=1,a;i<=N;i++) {
        cin>>a;
        int mask = 0;
        for(int j=0;j<primes.size();j++) if(a%primes[j] == 0) mask |= (1<<j);
        
        for(int j=i-1;j>=0;j--) for(int k=1;k<512;k++) if(ex[j][k] && (k&mask)) {
            ex[j+1][k&mask] = 1;
            if(k != mask) base[k] = 1;
        }
    }
    
    for(int k=1;k<512;k++) if(!base[k]) {
        for(int j=N;j>=0;j--) if(ex[j][k]) {
            if(j&1) return cout<<"First",0;
            break;
        }
    }
    cout<<"Second";

}
```
