```cpp
#include <bits/stdc++.h>
using namespace std;

int N,M,A,B,a[1000][1000]{},v[1000][1000]{};
int dx[4] = {1,0,-1,0};
int dy[4] = {0,1,0,-1};

int main(){
	cin.tie(0)->sync_with_stdio(0);
	
	cin>>M>>N>>B>>A;
	for(int i=0;i<N;i++) for(int j=0;j<M;j++) cin>>a[i][j];
	vector<pair<int,int>> r;
	queue<pair<int,int>> q;
	q.emplace(A,B);
	v[A][B]++;
	while(!q.empty()){
		auto [x,y] = q.front(); q.pop();
		r.emplace_back(x,y);
		for(int i=0;i<4;i++){
			int xx=x+dx[i], yy=y+dy[i];
			if(xx<0 || xx>=N || yy<0 || yy>=M || v[xx][yy] || a[xx][yy]!=a[A][B]) continue;
			q.emplace(xx,yy);
			v[xx][yy]++;
		}
	}
	sort(r.begin(),r.end());
	for(auto [x,y]:r) cout<<y<<' '<<x<<'\n';

}
```