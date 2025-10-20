```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int Q;
multiset<string> a, b;

int main() {
    cin.tie(0)->sync_with_stdio(0);
    
    cin>>Q;
    for(string o, s;Q--;) {
        cin>>o>>s;
        if(o == "find") {
            ll ans = 0;
            string tmp = "";
            int acnt[1000]{};
            for(int i=0;i<s.size()-1;i++) {
                tmp += s[i];
                acnt[i] = a.count(tmp);
            }
            tmp = "";
            reverse(s.begin(), s.end());
            for(int i=0;i<s.size()-1;i++) {
                tmp += s[i];
                ans += acnt[s.size()-2-i] * b.count(tmp);
            }
            cout<<ans<<'\n';
        }
        else {
            bool rev = s == "B";
            bool add = o == "add";
            auto &c = rev ? b : a;
            cin>>s;
            if(rev) reverse(s.begin(), s.end());
            
            string tmp = "";
            for(char j:s) {
                tmp += j;
                if(add) c.insert(tmp);
                else c.erase(c.find(tmp));
            }
        }
    }

}
```
