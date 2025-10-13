# segtree
```cpp
#pragma GCC optimize("O3, unroll-loops")
#include <bits/stdc++.h>
using namespace std;

int T, N, a[3000001]{}, mn[8388608]{}, mx[8388608]{}, ans = 1;

void init(int s, int e, int n) {
    if(s == e) {
        mn[n] = mx[n] = a[s];
        return;
    }
    int m = (s+e)>>1;
    init(s,m,n<<1); init(m+1,e,(n<<1)|1);
    mn[n] = min(mn[n<<1], mn[(n<<1)|1]);
    mx[n] = max(mx[n<<1], mx[(n<<1)|1]);
}

int f(int s, int e, int l, int r, int n) {
    if(l>r || l>e || r<s) return 2e9;
    if(l<=s && e<=r) return mn[n];
    int m = (s+e)>>1;
    return min(f(s,m,l,r,n<<1), f(m+1,e,l,r,(n<<1)|1));
}

int g(int s, int e, int l, int r, int n) {
    if(l>r || l>e || r<s) return 0;
    if(l<=s && e<=r) return mx[n];
    int m = (s+e)>>1;
    return max(g(s,m,l,r,n<<1), g(m+1,e,l,r,(n<<1)|1));
}

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>T>>N;
    for(int i=1;i<=N;i++) cin>>a[i];
    init(1,N,1);
    
    for(int i=1,j=1;i<=N;i++) {
        while(j<i && g(1,N,j,i,1) - f(1,N,j,i,1) > T) j++;
        ans = max(ans, i-j+1);
    }
    cout<<ans;

}
```

# deque
```cpp
#include <bits/stdc++.h>
using namespace std;

int T, N, ans = 1;
deque<pair<int, int>> mx, mn;

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>T>>N;
    for(int i=1,j=1,a;i<=N;i++) {
        cin>>a;
        while(!mn.empty() && mn.back().first > a) mn.pop_back();
        mn.emplace_back(a,i);
        while(!mx.empty() && mx.back().first < a) mx.pop_back();
        mx.emplace_back(a,i);
        while(j<i && mx.front().first - mn.front().first > T) {
            j++;
            while(mx.front().second < j) mx.pop_front();
            while(mn.front().second < j) mn.pop_front();
        }
        ans = max(ans, i-j+1);
    }
    cout<<ans;

}
```
