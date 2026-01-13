```cpp
#include <bits/stdc++.h>
using namespace std;

int N;
int arr[1000002]{};
int left_max1[1000002]{}, left_max2[1000002]{};
int right_max1[1000002]{}, right_max2[1000002]{};

int main() {
    cin.tie(0)->sync_with_stdio(0);

    cin>>N;
    for(int i=1;i<=N;i++) cin>>arr[i];
    for(int i=1;i<=N;i++) {
        left_max1[i] = max(left_max1[i-1], arr[i]);
        if(i>1) left_max2[i] = max(left_max2[i-1], arr[i]);
    }
    for(int i=N;i>=1;i--) {
        right_max1[i] = max(right_max1[i+1], arr[i]);
        if(i<N) right_max2[i] = max(right_max2[i+1], arr[i]);
    }

    int ans = 1e9;
    for(int i=2;i<=N-2;i++) {
        int left_result = min(arr[1] + left_max2[i], left_max1[i-1] + arr[i]);
        int right_result = min(arr[i+1] + right_max1[i+2], right_max2[i+1] + arr[N]);
        ans = min(ans, left_result + right_result);
    }

    cout<<ans;

}
```
