```cpp
#pragma GCC optimize("Ofast")
#pragma GCC optimize("unroll-loops")
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

ll N, Q, sq=1359;
pair<ll, ll> seg[262144]{};
ll a[100001]{}, cnt[100001]{}, q1[100001]{};

pair<ll, ll> operator+(pair<ll, ll> a, pair<ll, ll> b) {
    return {a.first + b.first, a.second + b.second};
}

void upd(int s, int e, int i, ll v, int n) {
    if(s == e) {
        seg[n].first += v;
        seg[n].second += v*s;
        return;
    }
    int m = (s+e)>>1;
    if(i<=m) upd(s,m,i,v,n<<1);
    else upd(m+1,e,i,v,(n<<1)+1);
    seg[n] = seg[n<<1] + seg[(n<<1)+1];
}

pair<ll, ll> find(int s, int e, int l, int r, int n) {
    if(l>r || l>e || r<s) return {0,0};
    if(l<=s && e<=r) return seg[n];
    int m = (s+e)>>1;
    return find(s,m,l,r,n<<1) + find(m+1,e,l,r,(n<<1)+1);
}

int main() {
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N;
    for(int i=1;i<=N;i++) {
        cin>>a[i];
        cnt[a[i]]++;
        upd(1,100000,a[i],1,1);
    }

    for(int i=1;i<sq;i++) for(int j=1;j<=N;j++) q1[i] += a[j] % i;

    for(cin>>Q;Q--;) {
        int op, i, x;
        cin>>op;
        if(op == 3) {
            cin>>i>>x;
            ll prev = a[i];
            for(int k=1;k<sq;k++) q1[k] += x%k - prev%k;
            cnt[prev]--;
            cnt[x]++;
            a[i] = x;
            upd(1,100000,prev,-1,1);
            upd(1,100000,x,1,1);
        }
        else {
            cin>>x;
            if(op == 1) {
                if(x < sq) cout<<q1[x]<<'\n';
                else {
                    ll ans = 0;
                    for(int k=1;(k-1)*x<=100000;k++) {
                        auto [c,s] = find(1,100000,max(1,(k-1)*x), min(100000,k*x-1),1);
                        ans += s - c*(k-1)*x;
                    }
                    cout<<ans<<'\n';
                }
            }
            else {
                ll ans = N*x;
                if(x <= 4) {
                    for(int p=1;p<=x;p++) ans -= cnt[p] * (x/p) * p;
                }
                else {
                    ans -= cnt[1] * x;
                    ll prev = x, last = x+1, p = 2;
                    for(;p<=x/p;p++) {
                        ll q = x/p;
                        ll s = find(1,100000,q+1,prev,1).second;
                        ans -= s*(p-1);
                        ans -= cnt[p] * q * p;
                        prev = q;
                        last = q+1;
                    }
                    if(p < last) {
                        ans -= find(1,100000,p,last-1,1).second*(p-1);
                    }
                }
                cout<<ans<<'\n';
            }
        }
    }

}
```
