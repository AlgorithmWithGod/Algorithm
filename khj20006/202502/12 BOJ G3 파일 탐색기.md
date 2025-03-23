```java

import java.util.*;
import java.io.*;
import java.math.BigInteger;

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
	static List<String>[] arr;
	static int N;
	static HashMap<String, Integer> hash;
	static List<String> temp;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		arr = new List[N];
		temp = new ArrayList<>();
		for(int i=0;i<N;i++) {
			arr[i] = new ArrayList<>();
			String number = "";
			for(char c:br.readLine().toCharArray()) {
				if(('A'<=c && c<='Z') || ('a'<=c && c<='z')) {
					if(!number.equals("")) {
						arr[i].add(number);
						temp.add(number);
					}
					arr[i].add(""+c);
					number = "";
				}
				else {
					number += c;
				}
			}
			if(!number.equals("")) {
				arr[i].add(number);
				temp.add(number);
			}
			
		}
		
		hash = new HashMap<>();
		
		Collections.sort(temp, (p,q) -> {
			BigInteger a = new BigInteger(p);
			BigInteger b = new BigInteger(q);
			if(a.compareTo(b) == 1) return 1;
			if(a.compareTo(b) == -1) return -1;
			int a_zeros = 0, b_zeros = 0;
			for(char c:p.toCharArray()) {
				if(c != '0') break;
				a_zeros++;
			}
			for(char c:q.toCharArray()) {
				if(c != '0') break;
				b_zeros++;
			}
			return a_zeros-b_zeros;
		});
		
		int num = 1;
		String prev = "a";
		for(String i : temp) {
			if(i == prev) continue;
			hash.put(i, num++);
			prev = i;
		}
		bw.flush();
		
		for(int i=0;i<26;i++) {
			hash.put(""+(char)(i+65), num++);
			hash.put(""+(char)(i+97), num++);
		}
		
		
	}
	
	static void solve() throws Exception{
		
		Arrays.sort(arr,(a,b) -> {
			
			for(int i=0;i<Math.min(a.size(), b.size());i++) {
				int valA = hash.get(a.get(i)), valB = hash.get(b.get(i));
				if(valA-valB < 0) return -1;
				if(valA-valB > 0) return 1;
			}
			return a.size()-b.size();
			
		});
		
		for(List<String> L:arr) {
			for(String i:L) bw.write(i);
			bw.write("\n");
		}
		
	}
	
}

```
