```cpp
#include <bits/stdc++.h>
using namespace std;

int N;
bitset<131072> v;
int cnt[17]{};

void bck(int state) {
    if(v[state]) return;
    v[state].flip();
    for(int i=0;i<17;i++) if(!(state & (1<<i))) {
        bck(state | (1<<i));
    }
}

int main() {
    cin.tie(0)->sync_with_stdio(0);

    v[131071].flip();

    cin>>N;
    for(int i=0;i<N;i++) {
        string a;
        cin>>a;
        int state = 0;
        for(char c : a) state |= (1<<(c-'a'));
        bck(state);
    }
    
    string str;
    cin>>str;
    long long ans = 0;
    int state = 0;
    for(int i=0,j=-1;i<str.size();i++) {
        while(j<(int)str.size()-1 && !v[state]) {
            j++;
            if(!cnt[str[j]-'a']++) state |= (1<<(str[j]-'a'));
        }
        if(v[state]) ans += str.size() - j;
        if(!--cnt[str[i]-'a']) state ^= (1<<(str[i]-'a'));
    }
    
    cout<<ans;

}
```
