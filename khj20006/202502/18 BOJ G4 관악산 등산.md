```cpp

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main(){
    cin.tie(0)->sync_with_stdio(0);

    int D[5001]{}, H[5001]{};
    vector<vector<int>> V(5001);
    pair<int, int> A[5001]{};

    int N, M;
    cin>>N>>M;
    for(int i=1;i<=N;i++) cin>>H[i], A[i] = {H[i], i};
    sort(A+1, A+N+1, greater<>());

    for(int a,b;M--;){
        cin>>a>>b;
        if(H[a] < H[b]) swap(a,b);
        V[a].push_back(b);
    }

    for(int i=1;i<=N;i++) {
        for(int j:V[A[i].second]) D[j] = max(D[j], D[A[i].second] + 1);
    }

    for(int i=1;i<=N;i++) cout<<D[i]+1<<'\n';

}

```
