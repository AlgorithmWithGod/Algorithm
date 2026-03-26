```java
import java.util.*;
import java.io.*;

public class Main{
	static int N, M;
	static int[] Order;
	static class UF{
		int[] roots;
		int[] sizes;
		UF(int n){
			roots = new int[n];
			sizes = new int[n];
			for(int i = 0; i < n; i++){
				roots[i] = i;
				sizes[i] = 1;
			}
		}
		int getRoot(int target){
			while(true){
				int temp = roots[target];
				if(temp == target)
					return temp;
				target = temp;
			}

		}
		void union(int a1, int a2){
			int r1 = getRoot(a1);
			int r2 = getRoot(a2);
			if(r1 == r2) return;
			if(sizes[r1] >= sizes[r2]){
				roots[r2] = r1;
				sizes[r1] += sizes[r2];
			}else{
				roots[r1] = r2;
				sizes[r2] += sizes[r1];
			}
		}
		boolean connected(int a1, int a2){
			return getRoot(a1) == getRoot(a2);

		}
	}

	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		Order = new int[N];
		UF uf = new UF(N);
		for(int m = 0; m < M; m++){
			st = new StringTokenizer(br.readLine());
			int a1 = Integer.parseInt(st.nextToken()) - 1;
			int a2= Integer.parseInt(st.nextToken())-1;
			uf.union(a1, a2);

		}
		st = new StringTokenizer(br.readLine());
		int prev = Integer.parseInt(st.nextToken())-1;
		int prevRoot = uf.getRoot(prev);
		int answer = 0;
		// System.out.println("DEBUG: ");
		while(st.hasMoreTokens()){
			// System.out.println("DEBUG: ");
			int now = Integer.parseInt(st.nextToken())-1;
			int nowRoot = uf.getRoot(now);
			if(prevRoot != nowRoot)
				answer++;
			prev = now;
			prevRoot = nowRoot;
		}
		System.out.println(answer);
		br.close();
	}
}
```
