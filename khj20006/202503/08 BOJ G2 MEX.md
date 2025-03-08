## JAVA
```java

import java.util.*;
import java.io.*;


class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static long nextLong() {return Long.parseLong(st.nextToken());}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field

	static int N;
    static boolean[] A = new boolean[2200001];
    static boolean[] B = new boolean[2200001];
    
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
        for(nextLine();N-->0;A[nextInt()]=true);
		
	}
	
	static void solve() throws Exception{
		
		for(int i=0;i<=2200000;i++) {
            if(!A[i] && !B[i]){
                bw.write(i + "\n");
                return;
            }
            if(i<2 || !A[i]) continue;
            for(long j=i*2;j<=Math.min(2200000L,(long)i*i);j+=i) B[(int)j] = true;
        }
		
	}
	
}

```

## C++
```cpp

#include <iostream>
#include <bitset>
using namespace std;
using ll = long long;

int main() {
    cin.tie(0)->sync_with_stdio(0);

    int N;
    cin>>N;
    bitset<2200001> A, B;
    for(int a;N--;A[a]=1) cin>>a;
    for(int i=0;i<2200001;i++) {
        if(!A[i] && !B[i]) return cout<<i,0;
        if(i < 2 || !A[i]) continue;
        for(ll j=i*2;j<=min(2200000LL, (ll)i*i);j+=i) B[j] = 1;
    }

}

```
