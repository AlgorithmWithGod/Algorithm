```cpp
#pragma GCC optimize("O3, unroll-loops")
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int N, M, Q, bucketSize;
vector<pair<int,int>> edges;
vector<tuple<int,int,int>> queries;
int res[100000]{};

// disjoint set
int root[100001]{}, cnt[100001]{};
ll ans = 0;
vector<tuple<int,int,int>> works;
ll g(ll x) { return x*(x-1)/2; }
void u(int a, int b) {
    int x = a, y = b;
    while(x != root[x]) x = root[x];
    while(y != root[y]) y = root[y];
    if(x == y) {
        works.emplace_back(-1,-1,-1);
        return;
    }
    if(cnt[x] > cnt[y]) swap(x,y);
    works.emplace_back(x,y,cnt[x]);
    ans -= g(cnt[x]) + g(cnt[y]);
    cnt[y] += cnt[x];
    ans += g(cnt[y]);
    root[x] = y;
}
void rollback() {
    auto [x,y,r] = works.back(); works.pop_back();
    if(x == -1) return;
    ans -= g(cnt[y]);
    cnt[y] -= r;
    ans += g(cnt[x]) + g(cnt[y]);
    root[x] = x;
}

// odc
int lifetime[100000]{};
vector<int> infos[262144];
int need[100000]{};
void update(int s, int e, int l, int r, int n, int i) {
    if(l>r || l>e || r<s) return;
    if(l<=s && e<=r) {
        infos[n].push_back(i);
        return;
    }
    int m = (s+e)>>1;
    update(s,m,l,r,n*2,i);
    update(m+1,e,l,r,n*2+1,i);
}
void clear(int s, int e, int n) {
    for(int i:infos[n]) {
        auto [a,b] = edges[i];
        u(a,b);
    }
    if(s == e) {
        res[need[s]] = ans;
    }
    else {
        int m = (s+e)>>1;
        clear(s,m,n*2);
        clear(m+1,e,n*2+1);
    }
    for(int i=0;i<infos[n].size();i++) rollback();
}

int main() {
    cin.tie(0)->sync_with_stdio(0);
    cout.tie(0);

    cin>>N>>M>>Q;
    bucketSize = sqrt(M);
    iota(root, root+N+1, 0);
    fill(cnt, cnt+N+1, 1);

    edges.resize(M);
    for(auto &[a,b]:edges) cin>>a>>b;

    queries.resize(Q);
    int tmp = 0;
    for(auto &[a,b,c]:queries) cin>>a>>b, a--, b--, c=tmp++;

    sort(queries.begin(), queries.end(), [](auto a, auto b) -> bool{
        auto [al, ar, ax] = a;
        auto [bl, br, bx] = b;
        int anum = al/bucketSize, bnum = bl/bucketSize;
        if(anum == bnum) {
            if(anum & 1) return br < ar;
            return ar < br;
        }
        return anum < bnum;
    });

    fill(lifetime, lifetime + M, -1);
    int pl = 0, pr = 0, px = 0;
    for(int i=0;i<Q;i++) {
        auto [l, r, x] = queries[i];
        need[i] = x;
        if(i == 0) {
            pl = l, pr = r, px = x;
            for(int j=l;j<=r;j++) lifetime[j] = i;
        }
        else {
            while(pl<l) {
                if(pl<=pr && lifetime[pl] != -1) update(0,Q-1,lifetime[pl],i-1,1,pl);
                lifetime[pl++] = -1;
            }
            while(l<pl) if(lifetime[--pl] == -1) lifetime[pl] = i;
            while(pr<r) {
                if(++pr>=l && lifetime[pr] == -1) lifetime[pr] = i;
            }
            while(r<pr) {
                if(lifetime[pr] != -1) update(0,Q-1,lifetime[pr],i-1,1,pr);
                lifetime[pr--] = -1;
            }
        }
    }
    for(int i=0;i<M;i++) if(lifetime[i] != -1) update(0,Q-1,lifetime[i],Q-1,1,i);
    clear(0,Q-1,1);
    for(int i=0;i<Q;i++) cout<<res[i]<<'\n';

}
```
