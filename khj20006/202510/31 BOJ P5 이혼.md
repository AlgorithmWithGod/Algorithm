```cpp
#include <bits/stdc++.h>
using namespace std;

int N, arr[24]{}, ans = 0;
map<int, int> le;

void init() {
    for(int i=0;i<N;i++) cin>>arr[i];
    ans = 0;
    le = map<int, int>();
}

void fillLeft(int pos, int tar, int cur, int sum) {
    le[cur] = max(le[cur], sum);
    if(pos == tar) return;
    fillLeft(pos+1, tar, cur, sum);
    sum += arr[pos];
    fillLeft(pos+1, tar, cur+arr[pos], sum);
    fillLeft(pos+1, tar, cur-arr[pos], sum);
}

void checkRight(int pos, int tar, int cur, int sum) {
    if(le.find(cur) != le.end()) ans = max(ans, le[cur] + sum);
    if(pos == tar) return;
    checkRight(pos+1, tar, cur, sum);
    sum += arr[pos];
    checkRight(pos+1, tar, cur+arr[pos], sum);
	checkRight(pos+1, tar, cur-arr[pos], sum);
}

int solve() {
    fillLeft(0,N>>1,0,0);
    checkRight(N>>1,N,0,0);
    int sum = 0;
    for(int i=0;i<N;i++) sum += arr[i];
    return sum - ans;
}

int main() {
    cin.tie(0)->sync_with_stdio(0);
    
    for(cin>>N;N;cin>>N) {
        init();
        cout<<solve()<<'\n';
    }

}
```
