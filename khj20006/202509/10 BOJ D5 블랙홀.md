## Python
```python
import sys
from functools import cmp_to_key
input = sys.stdin.readline

def ccw(a,b,c):
    ax, ay = a
    bx, by = b
    cx, cy = c
    res = ax*by + bx*cy + cx*ay - (ax*cy + bx*ay + cx*by);
    if res > 0:
        return 1
    if res < 0:
        return -1
    return 0
    
def cmpe(a, b):
    ax, ay = a
    bx, by = b
    anum = 10
    bnum = 10
    if ax == 0:
        if ay > 0:
            anum = 2
        else:
            anum = 6
    elif ay == 0:
        if ax > 0:
            anum = 0
        else:
            anum = 4
    else:
        if ax > 0:
            if ay > 0:
                anum = 1
            else:
                anum = 7
        else:
            if ay > 0:
                anum = 3
            else:
                anum = 5
    
    if bx == 0:
        if by > 0:
            bnum = 2
        else:
            bnum = 6
    elif by == 0:
        if bx > 0:
            bnum = 0
        else:
            bnum = 4
    else:
        if bx > 0:
            if by > 0:
                bnum = 1
            else:
                bnum = 7
        else:
            if by > 0:
                bnum = 3
            else:
                bnum = 5
    
    if anum == bnum:
        return -ccw([0,0], a, b)
    return anum-bnum



N, M, K = map(int, input().split())
X, Y = map(int, input().split())

hull = []
for i in range(N):
    a, b = map(int, input().split())
    a -= X
    b -= Y
    hull.append([a,b])

tmp = []
for i in range(M):
    a, b = map(int, input().split())
    a -= X
    b -= Y
    if a == 0 and b == 0:
        K -= 1
    else:
        tmp.append([a,b])
        
if K <= 0:
    print(0)
    exit(0)

arr = sorted(tmp, key=cmp_to_key(cmpe))

t = []
e = 0
while e < N:
    p = (e+N-1)%N
    r1 = ccw([0,0], hull[p], arr[0])
    r2 = ccw([0,0], arr[0], hull[e])
    if r1 > 0 and r2 >= 0:
        break
    e+=1
e%=N

for g in arr:
    x, y = g
    while ccw([0,0], hull[(e+N-1)%N], [x,y]) <= 0 or ccw([0,0], [x,y], hull[e]) < 0:
        e = (e+1)%N
    l = 0
    r = 5000000000000000000
    m = (l+r)//2
    while l<r:
        sx, sy = hull[(e+N-1)%N]
        ex, ey = hull[e]
        res = ccw([x,y], [sx*(m+1),sy*(m+1)], [ex*(m+1),ey*(m+1)])
        if res < 0:
            l = m+1
        else:
            r = m
        m = (l+r)//2
    t.append(m)

R = sorted(t)
print(R[K-1])
```

## Java
```java
import java.io.*;
import java.math.BigInteger;
import java.util.*;

class IOController {
	BufferedReader br;
	BufferedWriter bw;
	StringTokenizer st;

	public IOController() {
		br = new BufferedReader(new InputStreamReader(System.in));
		bw = new BufferedWriter(new OutputStreamWriter(System.out));
		st = new StringTokenizer("");
	}

	String nextLine() throws Exception {
		String line = br.readLine();
		st = new StringTokenizer(line);
		return line;
	}

	String nextToken() throws Exception {
		while (!st.hasMoreTokens())
			nextLine();
		return st.nextToken();
	}

	int nextInt() throws Exception {
		return Integer.parseInt(nextToken());
	}

	long nextLong() throws Exception {
		return Long.parseLong(nextToken());
	}

	double nextDouble() throws Exception {
		return Double.parseDouble(nextToken());
	}

	void close() throws Exception {
		bw.flush();
		bw.close();
	}

	void write(String content) throws Exception {
		bw.write(content);
	}

}

class Point {
	long x, y;
	Point(long x, long y) {
		this.x = x;
		this.y = y;
	}
}

public class Main {

	static IOController io;

	//

	static int N, M, K;
	static List<Point> points;

	// 1 : counter-clockwise
	// -1 : clockwise
	// 0 : line
	static int ccw(Point a, Point b, Point c) {
		BigInteger ax = new BigInteger(Long.toString(a.x));
		BigInteger ay = new BigInteger(Long.toString(a.y));
		BigInteger bx = new BigInteger(Long.toString(b.x));
		BigInteger by = new BigInteger(Long.toString(b.y));
		BigInteger cx = new BigInteger(Long.toString(c.x));
		BigInteger cy = new BigInteger(Long.toString(c.y));
		BigInteger res = ax.multiply(by)
			.subtract(bx.multiply(ay))
			.add(bx.multiply(cy))
			.subtract(cx.multiply(by))
			.add(cx.multiply(ay))
			.subtract(ax.multiply(cy));

		return res.compareTo(new BigInteger("0"));
	}

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		M = io.nextInt();
		K = io.nextInt();

		Point[] hull = new Point[N];
		List<Point> lower = new ArrayList<>();
		List<Point> upper = new ArrayList<>();
		long X = io.nextLong();
		long Y = io.nextLong();
		for(int i=0;i<N;i++) hull[i] = new Point(io.nextLong()-X, io.nextLong()-Y);
		for(int i=0;i<M;i++) {
			Point point = new Point(io.nextLong()-X, io.nextLong()-Y);
			if(point.x == 0 && point.y == 0) {
				K--;
				continue;
			}
			if(point.y > 0) upper.add(point);
			else lower.add(point);
		}

		// early stopping
		if(K <= 0) {
			io.write("0");
			return;
		}

		Collections.sort(upper, (a,b) -> -ccw(new Point(0,0), a, b));
		Collections.sort(lower, (a,b) -> -ccw(new Point(0,0), a, b));
		points = new ArrayList<>();
		for(Point point : upper) points.add(point);
		for(Point point : lower) points.add(point);

		List<Long> time = new ArrayList<>();
		int e = 0;
		while(e < N) {
			int p = (e+N-1)%N;
			int r1 = ccw(new Point(0,0), hull[p], points.get(0));
			int r2 = ccw(new Point(0,0), points.get(0), hull[e]);
			if(r1 > 0 && r2 >= 0) break;
			e++;
		}
		e %= N;

		for(int i=0;i<points.size();i++) {
			while(ccw(new Point(0,0), hull[(e+N-1)%N], points.get(i)) <= 0 || ccw(new Point(0,0), points.get(i), hull[e]) < 0) e = (e+1)%N;
			long l = 0, r = (long)4e9, m = (l+r)>>1;
			while(l<r) {
				long sx = hull[(e+N-1)%N].x, sy = hull[(e+N-1)%N].y;
				long ex = hull[e].x, ey = hull[e].y;
				int res = ccw(points.get(i), new Point(sx*(m+1), sy*(m+1)), new Point(ex*(m+1), ey*(m+1)));
				if(res < 0) l = m+1;
				else r = m;
				m = (l+r)>>1;
			}
			time.add(m);
		}

		Collections.sort(time);
		io.write(time.get(K-1) + "\n");

		io.close();

	}

}
```

## C++
```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int N, M, K;
vector<pair<__int128, __int128>> hull, arr;

int ccw(pair<__int128, __int128> a, pair<__int128, __int128> b, pair<__int128, __int128> c) {
    auto [ax, ay] = a;
    auto [bx, by] = b;
    auto [cx, cy] = c;
    __int128 res = (__int128)ax*(__int128)by + (__int128)bx*(__int128)cy + (__int128)cx*(__int128)ay - ((__int128)ax*(__int128)cy + (__int128)bx*(__int128)ay + (__int128)cx*(__int128)by);
    if(res > 0) return 1;
    if(res < 0) return -1;
    return 0;
}

int main() {
    cin.tie(0)->sync_with_stdio(0);
    cout.tie(0);

    ll X, Y;
    cin>>N>>M>>K>>X>>Y;
    hull.resize(N);
    for(auto &[a,b]:hull) {
        ll c,d;
        cin>>c>>d;
        a = c-X, b = d-Y;
    }
    for(int i=0;i<M;i++) {
        ll c,d;
        cin>>c>>d;
        __int128 x = c-X, y = d-Y;
        if(!x && !y) K--;
        else arr.emplace_back(x,y);
    }
    if(K <= 0) return cout<<0,0;

    sort(arr.begin(), arr.end(), [](auto a, auto b) -> bool {
        auto [ax, ay] = a;
        auto [bx, by] = b;
        int anum, bnum;
        if(ax == 0) {
            if(ay > 0) anum = 2;
            else anum = 6;
        }
        else if(ay == 0) {
            if(ax > 0) anum = 0;
            else anum = 4;
        }
        else {
            if(ax > 0) {
                if(ay > 0) anum = 1;
                else anum = 7;
            }
            else {
                if(ay > 0) anum = 3;
                else anum = 5;
            }
        }

        if(bx == 0) {
            if(by > 0) bnum = 2;
            else bnum = 6;
        }
        else if(by == 0) {
            if(bx > 0) bnum = 0;
            else bnum = 4;
        }
        else {
            if(bx > 0) {
                if(by > 0) bnum = 1;
                else bnum = 7;
            }
            else {
                if(by > 0) bnum = 3;
                else bnum = 5;
            }
        }

        if(anum == bnum) return ccw({0,0}, a, b) > 0;
        return anum < bnum;
    });

    vector<__int128> t;
    int e = 0;
    while(e < N) {
        int p = (e+N-1)%N;
        int r1 = ccw({0,0}, hull[p], arr[0]);
        int r2 = ccw({0,0}, arr[0], hull[e]);
        if(r1 > 0 && r2 >= 0) break;
        e++;
    }
    e %= N;

    for(auto [x,y]:arr) {
        while(ccw({0,0}, hull[(e+N-1)%N], {x,y}) <= 0 || ccw({0,0}, {x,y}, hull[e]) < 0) e = (e+1)%N;
        __int128 l = 0, r = (__int128)5e18, m = (l+r)>>1;
        while(l<r) {
            auto [sx, sy] = hull[(e+N-1)%N];
            auto [ex, ey] = hull[e];
            int res = ccw({x,y}, {sx*(m+1), sy*(m+1)}, {ex*(m+1), ey*(m+1)});
            if(res < 0) l = m+1;
            else r = m;
            m = (l+r)>>1;
        }
        t.push_back(m);
    }

    sort(t.begin(), t.end());
    cout<<(ll)t[K-1];

}
```
