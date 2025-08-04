```java
import java.util.*;
import java.io.*;

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
		while (!st.hasMoreTokens()) nextLine();
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

public class Main {

	static IOController io;

	//

	static int N;
	static List<Integer>[] arr;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		init();
		solve();

		io.close();

	}

	static void init() throws Exception {

		N = io.nextInt();
		arr = new List[N];
		for(int i=0;i<N;i++) arr[i] = new ArrayList<>();
		for(int i=0;i<2*N-1;i++) {
			int a = io.nextInt();
			arr[a%N].add(a);
		}

	}

	static void solve() throws Exception {

		for(int i:get(N,0)) io.write(i + " ");

	}

	static List<Integer> get(int count, int mod) {
		if(count == 2) {
			List<Integer> res = new ArrayList<>();
			// 짝수에서 찾기
			for(int i=0;i<N;i+=2) if(arr[i].size() > 0) {
				int temp1 = arr[i].remove(arr[i].size()-1);
				for(int j=0;j<N;j+=2) if(arr[j].size() > 0) {
					int temp2 = arr[j].remove(arr[j].size()-1);
					if((temp1+temp2)%N != mod){
						arr[j].add(temp2);
						continue;
					}
					res.add(temp1);
					res.add(temp2);
					return res;
				}
				arr[i].add(temp1);
			}
			for(int i=1;i<N;i+=2) if(arr[i].size() > 0) {
				int temp1 = arr[i].remove(arr[i].size()-1);
				for(int j=1;j<N;j+=2) if(arr[j].size() > 0) {
					int temp2 = arr[j].remove(arr[j].size()-1);
					if((temp1+temp2)%N != mod){
						arr[j].add(temp2);
						continue;
					}
					res.add(temp1);
					res.add(temp2);
					return res;
				}
				arr[i].add(temp1);
			}
			return res;
		}

		List<Integer> res3 = get(count/2, mod/2);
		List<Integer> res4 = get(count/2, mod/2);
		if(res3.isEmpty() || res4.isEmpty()) {
			for(int i:res3) arr[i%N].add(i);
			for(int i:res4) arr[i%N].add(i);
		}
		else {
			for(int i:res4) res3.add(i);
			return res3;
		}

		List<Integer> res5 = get(count/2, (mod+N)/2);
		List<Integer> res6 = get(count/2, (mod+N)/2);
		if(res5.isEmpty() || res6.isEmpty()) {
			for(int i:res5) arr[i%N].add(i);
			for(int i:res6) arr[i%N].add(i);
		}
		else {
			for(int i:res6) res5.add(i);
			return res5;
		}

		return new ArrayList<>();

	}

}
```
