```cpp
#include <bits/stdc++.h>
using namespace std;

int Q, MOD;
vector<int> pos[1000001]{};
stack<int> st;
set<int> s;

int main(){
	cin.tie(0)->sync_with_stdio(0);

	cin>>Q>>MOD;
	if(MOD > Q) {
		for(int o,a;Q--;) {
			cin>>o;
			if(o == 1) cin>>a;
			if(o == 3) cout<<"-1\n";
		}
		return 0;
	}

	for(int i=0,o,a;i<Q;i++) {
		cin>>o;
		if(o == 1) {
			cin>>a;
			a %= MOD;
			if(!pos[a].empty()) s.erase(pos[a].back());
			s.insert(st.size());
			pos[a].push_back(st.size());
			st.push(a);
		}
		else if(o == 2) {
			if(st.empty()) continue;
			a = st.top(); st.pop();
			s.erase(pos[a].back());
			pos[a].pop_back();
			if(!pos[a].empty()) s.insert(pos[a].back());
		}
		else {
			if(s.size() != MOD) cout<<"-1\n";
			else cout<<st.size()-(*s.begin())<<'\n';
		}
	}

}
```
