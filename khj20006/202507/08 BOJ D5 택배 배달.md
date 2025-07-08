```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

ll A[2001][201]{}, S[2001][201]{};
ll le[2001]{}, ri[2001]{};
ll dist[2001][2001]{}, up[2001][2001]{}, down[2001][2001]{}, mid[2001][2001]{};
pair<int, int> p[200002]{};

int main(){
    cin.tie(0)->sync_with_stdio(0);

    int R, C;
    cin>>R>>C;
    
    for(int i=1;i<=R;i++) {
        for(int j=1;j<=C;j++) {
            cin>>A[i][j];
            S[i][j] = S[i][j-1] + A[i][j];
        }
        le[i] = le[i-1] + A[i][1];
        ri[i] = ri[i-1] + A[i][C];
    }

    for(int j=1;j<=R;j++) {
        up[1][j] = S[1][C] + ri[j]-ri[1];
        up[j][1] = S[1][C] + le[j]-le[1];
    }
    for(int i=2;i<=R;i++) for(int j=2;j<=R;j++) {
        up[i][j] = min(up[i-1][j] + A[i][1], up[i][j-1] + A[j][C]);
        if(i<j) {
            up[i][j] = min(up[i][j], S[i][C] + ri[j]-ri[i]);
        }
        else{
            up[i][j] = min(up[i][j], S[j][C] + le[i]-le[j]);
        }
    }

    for(int j=1;j<=R;j++) {
        down[R][j] = S[R][C] + ri[R-1]-ri[j-1];
        down[j][R] = S[R][C] + le[R-1]-le[j-1];
    }
    for(int i=R-1;i>=1;i--) for(int j=R-1;j>=1;j--) {
        down[i][j] = min(down[i+1][j] + A[i][1], down[i][j+1] + A[j][C]);
        if(i<j) {
            down[i][j] = min(down[i][j], S[j][C] + le[j-1]-le[i-1]);
        }
        else{
            down[i][j] = min(down[i][j], S[i][C] + ri[i-1]-ri[j-1]);
        }
    }

    for(int i=1;i<=R;i++) mid[i][i] = S[i][C];
    for(int k=1;k<R;k++) for(int i=1;i+k<=R;i++) {
        int j = i+k;
        mid[i][j] = min({mid[i+1][j] + A[i][1], mid[i][j-1] + A[j][C], S[i][C] + ri[j]-ri[i], S[j][C] + le[j-1]-le[i-1]});
        mid[j][i] = min({mid[j-1][i] + A[j][1], mid[j][i+1] + A[i][C], S[i][C] + le[j]-le[i], S[j][C] + ri[j-1]-ri[i-1]});
    }

    for(int i=1;i<=R;i++) for(int j=1;j<=R;j++) {
        dist[i][j] = min({up[i][j], down[i][j], mid[i][j]});
    }

    p[0] = {1,1};
    int D;
    cin>>D;
    for(int i=1;i<=D;i++) cin>>p[i].first>>p[i].second;

    ll ans = A[1][1];
    for(int i=1;i<=D;i++) {
        auto [pr,pc] = p[i-1];
        auto [r,c] = p[i];

        if(pr == r) {
            if(pc < c) {
                ll res1 = S[r][c] - S[r][pc];
                ll res2 = dist[r][r] + max(0LL, S[r][C-1]-S[r][c-1]);
                if(pc == 1) res2 -= A[pr][1];
                else res2 += S[pr][pc-1]-S[pr][1];
                ans += min(res1, res2);
            }
            else{
                ll res1 = S[r][pc-1] - S[r][c-1];
                ll res2 = dist[r][r] + max(0LL, S[r][c]-S[r][1]);
                if(pc == C) res2 -= A[pr][C];
                else res2 += S[pr][C-1]-S[pr][pc];
                ans += min(res1, res2);
            }
        }
        else {
            // prev에서 왼쪽으로, cur에서 오른쪽으로
            ll res1 = dist[pr][r] + max(0LL, S[r][C-1]-S[r][c-1]);
            if(pc == 1) res1 -= A[pr][1];
            else res1 += S[pr][pc-1]-S[pr][1];
            // prev에서 오른쪽으로, cur에서 왼쪽으로
            ll res2 = dist[r][pr] + max(0LL, S[r][c]-S[r][1]);
            if(pc == C) res2 -= A[pr][C];
            else res2 += S[pr][C-1]-S[pr][pc];
            // prev에서 왼쪽으로, cur에서 왼쪽으로
            ll res3 = (pr<r ? le[r-1]-le[pr] : le[pr-1]-le[r]) + S[pr][pc-1] + S[r][c];
            // prev에서 오른쪽으로, cur에서 오른쪽으로
            ll res4 = (pr<r ? ri[r-1]-ri[pr] : ri[pr-1]-ri[r]) + S[pr][C]-S[pr][pc] + S[r][C]-S[r][c-1];
            
            ll res = min({res1, res2, res3, res4});
            
            ans += res;
        }

    }
    cout<<ans;

}
```
