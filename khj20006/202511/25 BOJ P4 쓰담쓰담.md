```cpp
#include <bits/stdc++.h>
using namespace std;

int N, Q;
int seg[262144]{}, height[100001]{};

void upt(int s, int e, int i, int n) {
    if(s == e) {
        if(s == N || height[s] <= height[s+1]) seg[n] = 0;
        else seg[n] = 1;
        return;
    }
    int m = (s+e)>>1;
    if(i <= m) upt(s,m,i,n<<1);
    else upt(m+1,e,i,n<<1|1);
    seg[n] = seg[n<<1] + seg[n<<1|1];
}

int find(int s, int e, int l, int r, int n) {
    if(l>r || l>e || r<s) return 0;
    if(l<=s && e<=r) return seg[n];
    int m = (s+e)>>1;
    return find(s,m,l,r,n<<1) + find(m+1,e,l,r,n<<1|1);
}

int main(){
    cin.tie(0)->sync_with_stdio(0);

    cin>>N>>Q;
    for(int i=1;i<=N;i++) cin>>height[i];
    for(int i=1;i<=N;i++) upt(1,N,i,1);

    for(int o,l,r;Q--;) {
        cin>>o>>l>>r;
        if(o == 1) cout<<(find(1,N,l,r-1,1) ? "HSS090\n": "CS204\n");
        else {
            swap(height[l], height[r]);
            if(l>1) upt(1,N,l-1,1);
            upt(1,N,l,1);
            if(r>1) upt(1,N,r-1,1);
            upt(1,N,r,1);
        }
    }

}
```
