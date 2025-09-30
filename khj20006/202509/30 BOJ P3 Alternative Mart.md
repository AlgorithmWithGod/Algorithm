```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M, K, Q;
vector<vector<pair<int, int>>> V(50001);
vector<deque<pair<int, int>>> D(50001);
priority_queue<tuple<int, int, int>, vector<tuple<int, int, int>>, greater<>> PQ;

int main() {
    cin.tie(0)->sync_with_stdio(0);

    for (cin >> N >> M >> K >> Q; K--;) {
        int a;
        cin >> a;
        PQ.emplace(0, a, a);
        D[a].emplace_back(0, a);
    }
    for (int a, b, c; M--; V[a].emplace_back(b, c), V[b].emplace_back(a, c)) cin >> a >> b >> c;

    while (!PQ.empty()) {
        auto [d, p, n] = PQ.top();    PQ.pop();
        bool con = false, ex = false;
        for (auto [_, q] : D[n]) {
            if (q == p) {
                ex = 1;
                if (d > _) con = 1;
            }
        }
        if (!ex) con = 1;
        if (con) continue;
        for (auto [i, c] : V[n]) {
            int org = -1;
            for (auto [_, q] : D[i]) {
                if (p == q) org = _;
            }
            stack<pair<int, int>> tmp;
            if (org == -1) {
                while (!D[i].empty() && D[i].back().first > d+c) {
                    tmp.push(D[i].back());
                    D[i].pop_back();
                }
                if (D[i].size() < 11) {
                    D[i].emplace_back(d + c, p);
                    PQ.emplace(d + c, p, i);
                }
                while (D[i].size() < 11 && !tmp.empty()) {
                    D[i].emplace_back(tmp.top());
                    tmp.pop();
                }
            }
            else if (d + c < org) {
                while (!D[i].empty() && D[i].back().first > d+c) {
                    if(D[i].back().second != p) tmp.push(D[i].back());
                    D[i].pop_back();
                }
                D[i].emplace_back(d + c, p);
                while (!tmp.empty()) {
                    D[i].emplace_back(tmp.top());
                    tmp.pop();
                }
                PQ.emplace(d + c, p, i);
            }
        }
    }

    for (int s, c, a; Q--;) {
        vector<int> t;
        for (cin >> s >> c; c--; t.push_back(a)) cin >> a;
        bool pr = false;
        for (int i = 0; i < D[s].size(); i++) {
            bool cant = false;
            for (int j : t) cant |= j == D[s][i].second;
            if (!cant) {
                pr = true;
                cout << D[s][i].second << ' ' << D[s][i].first << '\n';
                break;
            }
        }
    }

}
```
