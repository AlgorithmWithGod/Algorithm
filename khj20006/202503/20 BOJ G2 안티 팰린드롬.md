```java

import java.util.*;
import java.io.*;

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static String nextToken() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}
	static int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
	static long nextLong() throws Exception { return Long.parseLong(nextToken()); }
	static double nextDouble() throws Exception { return Double.parseDouble(nextToken()); }
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int[] cnt;
	static int N;
	static String ans;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		String s = br.readLine();
		N = s.length();
		cnt = new int[26];
		for(char c : s.toCharArray()) cnt[c-'a']++;
		
	}
	
	static void solve() throws Exception{

		for(int i=0;i<26;i++) if(cnt[i] > (N+1)/2) {
			bw.write("-1");
			return;
		}
		
		ans = new String();
		for(int i=0;i<26;i++) if(cnt[i] > 0) {
			if(ans.length() > (N+1)/2 || ans.length() + cnt[i] <= (N+1)/2) {
				while(cnt[i] > 0) {
					ans += (char)('a'+i);
					cnt[i]--;
				}
			}
			else if(N%2 == 1 && ans.length() == N/2) {
				while(cnt[i] > 0) {
					ans += (char)('a'+i);
					cnt[i]--;
				}
			}
			else {
				int need = 0;
				while(ans.length() < (N+1)/2) {
					ans += (char)('a'+i);
					need++;
				}
				cnt[i] -= need;
				if(N%2 == 1) need--;
				
				for(int j=i+1;j<26;j++) while(cnt[j] > 0 && need > 0) {
					cnt[j]--;
					ans += (char)('a'+j);
					need--;
				}
				while(cnt[i] > 0) {
					ans += (char)('a'+i);
					cnt[i]--;
				}
				
			}
		}
		bw.write(ans);

	}
	
}

```
