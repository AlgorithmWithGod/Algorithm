```cpp

#include <bits/stdc++.h>
using namespace std;

using ld = long double;

int main(){
  cin.tie(0)->sync_with_stdio(0);
  
  int theta, N;
  cin>>theta>>N;
  vector<pair<int,int>> A(N);
  for(auto &[x,h]:A) cin>>x>>h;
  sort(A.begin(), A.end());
  
  ld t = tan(M_PI * theta / 180.);
  ld ans = 0, last = -1;
  for(int i=0;i<N;i++){
    int x = A[i].first, h = A[i].second;
    ld pos = (ld)h / t;
    if(last > pos+x) continue;
    if(last > x) ans += pos+x-last;
    else ans += pos;
    last = pos+x;
  }
  cout<<ans;
  
}

```
