```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Iterator;
import java.util.StringTokenizer;

public class Main {
	private static class WeightedUF{
		int[] ids;
		int[] size;
		public WeightedUF(int v) {
			ids = new int[v];
			size = new int[v];
			for (int i = 0; i < ids.length; i++) {
				ids[i] = i;
				size[i] = 1;
			}
		}
		public int root(int a) {
			while(a != ids[a])
				a = ids[a];
			return a;
		}
		public void union(int a, int b) {
			int g, l;
			if(size[a] >= size[b]) {
				g = a;
				l = b;
			}else {
				l = a;
				g = b;
			}
			// b가 더 깊이가 짧음
			ids[root(b)] = root(a);
		}
		public boolean connected(int a, int b) {
			return root(a) == root(b);
		}
	}
	private static BufferedReader br;
	private static Main.WeightedUF uf;
	private static int m;
	private static int n;
	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
		String[] temp = br.readLine().split(" ");
		n = Integer.parseInt(temp[0])+1;
		m = Integer.parseInt(temp[1]);
		uf = new WeightedUF(n);
		
		for(int i = 0; i<m; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			int command = Integer.parseInt( st.nextToken());
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			if(command == 0) {
				// 합집합
				uf.union(a, b);
			}else {
				// conneted()
				if(uf.connected(a, b))
					sb.append("YES\n");
				else
					sb.append("NO\n");
			}
		}
		System.out.println(sb.toString());
		br.close();
	}
 

}
```
