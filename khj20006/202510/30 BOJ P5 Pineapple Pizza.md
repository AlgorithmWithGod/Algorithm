```cpp
#include <bits/stdc++.h>
using namespace std;

vector<pair<int, int>> p, u, l;
int N, K;

int ccw(pair<long long, long long> a, pair<long long, long long> b, pair<long long, long long> c) {
    auto [ax, ay] = a;
    auto [bx, by] = b;
    auto [cx, cy] = c;
    long long res = ax*by + bx*cy + cx*ay - (ax*cy + bx*ay + cx*by);
    if(res > 0) return 1;
    if(res < 0) return -1;
    return 0;
}

int main() {
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>N>>K;
    if(N%K) return cout<<"NO",0;
    p.resize(N);
    for(auto &[x,y]:p) cin>>x>>y;
    int _x, _y;
    cin>>_x>>_y;
    for(auto &[x,y]:p) {
        x-=_x, y-=_y;
        if(y < 0 || (y == 0 && x < 0)) l.emplace_back(x,y);
        else u.emplace_back(x,y);
    }

    sort(u.begin(), u.end(), [](auto a, auto b) -> bool {
        return ccw({0,0}, a, b) < 0;
    });
    sort(l.begin(), l.end(), [](auto a, auto b) -> bool {
        return ccw({0,0}, a, b) < 0;
    });
    
    deque<int> a;
    for(int i=1;i<u.size();i++) {
        int cnt = 1;
        while(i<u.size() && !ccw({0,0}, u[i-1], u[i])) cnt++, i++;
        a.push_back(cnt);
    }
    for(int i=1;i<l.size();i++) {
        int cnt = 1;
        while(i<l.size() && !ccw({0,0}, l[i-1], l[i])) cnt++, i++;
        a.push_back(cnt);
    }
    
    for(int c=0;c<N;c++) {
        a.push_back(a.front());
        a.pop_front();
        int cur = 0;
        bool poss = 1;
        for(int i:a) {
            cur += i;
            if(cur == N/K) cur = 0;
            else if(cur > N/K) {
                poss = 0;
                break;
            }
        }
        if(poss) return cout<<"YES", 0;
    }
    cout<<"NO";

}
```
