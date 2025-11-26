```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int Q;
ll G, L, X;
vector<ll> g, l, x, r1, r2;

void bck(int pos, int tar, ll cur, vector<ll> &r) {
    if(pos == tar) {
        if(cur > 1) r.push_back(cur);
        return;
    }
    bck(pos+1, tar, cur, r);
    cur *= x[pos];
    bck(pos+1, tar, cur, r);
}

int main(){
    cin.tie(0)->sync_with_stdio(0);

    for(cin>>Q;Q--;) {
        int n1, n2;
        
        cin>>n1;
        g.resize(n1);
        G = 1;
        for(ll &i : g) {
            cin>>i;
            G *= i;
        }

        cin>>n2;
        l.resize(n2);
        L = 1;
        for(ll &i : l) {
            cin>>i;
            L *= i;
        }

        sort(g.begin(), g.end());
        sort(l.begin(), l.end());

        x = vector<ll>();
        for(ll i : g) for(auto it = l.begin(); it != l.end(); it++) {
            if(*it == i) {
                l.erase(it);
                break;
            }
        }
        
        for(int i=0;i<l.size();) {
            ll res = 1;
            int j=i;
            while(j<l.size() && l[i]==l[j]) res *= l[j++];
            x.push_back(res);
            i = j;
        }

        r1 = vector<ll>();
        r2 = vector<ll>();

        bck(0, x.size()/2, 1, r1);
        bck(x.size()/2, x.size(), 1, r2);

        sort(r1.begin(), r1.end());
        sort(r2.begin(), r2.end(), greater<>());

        ll sq = sqrtl(L/G);
        int idx = 0;
        ll mn = 1+L/G, ans1 = 1, ans2 = L/G;
        for(ll i : r1) {
            while(idx < r2.size() && i*r2[idx] >= sq) idx++;
            if(idx < r2.size()) {
                ll val = r2[idx]*i + L/G/(r2[idx]*i);
                ll aa = min(r2[idx]*i, L/G/(r2[idx]*i));
                ll bb = max(r2[idx]*i, L/G/(r2[idx]*i));
                if(val < mn || (val == mn && ans1 > aa)) {
                    ans1 = aa, ans2 = bb, mn = val;
                }
            }
            if(idx > 0) {
                ll val = r2[idx-1]*i + L/G/(r2[idx-1]*i);
                ll aa = min(r2[idx-1]*i, L/G/(r2[idx-1]*i));
                ll bb = max(r2[idx-1]*i, L/G/(r2[idx-1]*i));
                if(val < mn || (val == mn && ans1 > aa)) {
                    ans1 = aa, ans2 = bb, mn = val;
                }
            }
            {
                ll val = i + L/G/i;
                ll aa = min(i, L/G/i);
                ll bb = max(i, L/G/i);
                if(val < mn || (val == mn && ans1 > aa)) {
                    ans1 = aa, ans2 = bb, mn = val;
                }
            }
            idx = max(0, idx-1);
        }
        for(ll i : r2) {
            ll val = i + L/G/i;
            ll aa = min(i, L/G/i);
            ll bb = max(i, L/G/i);
            if(val < mn || (val == mn && ans1 > aa)) {
                ans1 = aa, ans2 = bb, mn = val;
            }
        }
        cout<<G*ans1<<' '<<G*ans2<<'\n';
        
    }

}
```
