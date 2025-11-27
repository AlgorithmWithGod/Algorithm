```cpp
#include <bits/stdc++.h>
using namespace std;

const int dx[4] = {1,0,-1,0};
const int dy[4] = {0,1,0,-1};

int R;

vector<pair<int, int>> office() {
    int N, M, X, Y;
    cin>>M>>N>>Y>>X;
    Y--, X--;

    int root[250000]{};
    int cnt[250000]{};
    iota(root, root+N*M, 0);
    fill(cnt, cnt+N*M, 1);
    function<int(int)> find = [&](int x) -> int { return x == root[x] ? x : root[x] = find(root[x]); };

    bitset<250000> vis;
    vis[X*M+Y] = 1;

    vector<tuple<int, int, int>> infos;
    for(int i=0;i<N;i++) for(int j=0;j<M;j++) {
        int a;
        cin>>a;
        infos.emplace_back(a,i,j);
    }

    sort(infos.begin(), infos.end());
    vector<pair<int, int>> events;
    for(int i=0;i<infos.size();) {
        auto [cc,aa,bb] = infos[i];
        int j = i;
        while(j<infos.size() && get<0>(infos[j]) == cc) {
            auto [c,a,b] = infos[j];
            vis[a*M+b] = 1;
            for(int k=0;k<4;k++) {
                int aa = a+dx[k], bb = b+dy[k];
                if(aa<0 || aa>=N || bb<0 || bb>=M || !vis[aa*M+bb]) continue;
                int x = find(a*M+b), y = find(aa*M+bb);
                if(x == y) continue;
                cnt[y] += cnt[x];
                root[x] = y;
            }
            j++;
        }
        i = j;
        events.emplace_back(cc, cnt[find(X*M+Y)]);
    }

    return events;
}

int main(){
    cin.tie(0)->sync_with_stdio(0);

    cin>>R;
    vector<pair<int, int>> res1 = office();
    vector<pair<int, int>> res2 = office();
    
    int ans = 2e9 + 1;
    for(auto [c,v] : res1) if(v >= R) {
        ans = min(ans, c);
        break;
    }
    for(auto [c,v] : res2) if(v >= R) {
        ans = min(ans, c);
        break;
    }
    for(int i=0,j=res2.size()-1;i<res1.size();i++) {
        if(res1[i].second + res2[j].second >= R) {
            while(j>=0 && res1[i].second + res2[j].second >= R) j--;
            j++;
        }
        if(res1[i].second + res2[j].second >= R) {
            ans = min(ans, res1[i].first + res2[j].first);
        }
    }
    cout<<ans;

}
```
