```java
import java.io.*;
import java.util.*;

public class boj7511 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static StringBuilder sb = new StringBuilder();

	static int n, m;
	static int[] parents;
	public static void main(String[] args) throws Exception {
		nextLine();
		int t = nextInt();
		for(int a = 1 ; a <= t ; a++){
            nextLine();
            n = nextInt();

            for(int i = 0 ; i < n ; i++) {
            	parents[i] = i;
            }

            nextLine();
            m = nextInt();

            for(int i = 0 ; i < m ; i++) {
            	nextLine();
                int v1 = nextInt();
                int v2 = nextInt();

                if(find(v1) != find(v2)) {
                    union(v1,v2);
                }
            }

            nextLine();
            int k = nextInt();

            sb.append("Scenario "+a+":\n");

            for(int i = 0 ; i < k ; i++){
            	nextLine();
                int v1 = nextInt();
                int v2 = nextInt();

                if(find(v1) == find(v2)) {
                    sb.append("1\n");
                }else{
                    sb.append("0\n");
                }
            }sb.append("\n");
        }

        System.out.println(sb);
        br.close();
    }
	
	static int find(int x) {
        if(x == parents[x])
            return parents[x];

        return parents[x] = find(parents[x]);
    }

    static void union(int x,int y) {
        x = find(x);
        y = find(y);

        if(x < y)
        	parents[y] = x;
        else
        	parents[x] = y;
    }
}
```
