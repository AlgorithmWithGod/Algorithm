```java
import java.util.*;
import java.io.*;

public class boj1240 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static ArrayList<Node>[] map;
    static boolean[] visit;
    static int n;
    static int max;

    public static void main(String[] args) throws Exception {
    	nextLine();
        n = nextInt();
        int m = nextInt();
        map = new ArrayList[n];
        visit = new boolean[n];

        for (int i = 0; i < n; i++) {
            map[i] = new ArrayList<>();
        }

        for (int i = 0; i < n - 1; i++) {
        	nextLine();
            int a = nextInt() - 1;
            int b = nextInt() - 1;
            int d = nextInt();
            map[a].add(new Node(b, d));
            map[b].add(new Node(a, d));
        }

        for (int i = 0; i < m; i++) {
        	nextLine();
            int a = nextInt() - 1;
            int b = nextInt() - 1;
            dfs(a, b, 0);
            System.out.println(max);
            max = 0;
            visit = new boolean[n];
        }
    }

    static void dfs(int start, int end, int dist) {
        if (start == end) {
            max = dist;
            return;
        }

        visit[start] = true;
        for (int i = 0; i < map[start].size(); i++) {
            if (!visit[map[start].get(i).next]) {
                dfs(map[start].get(i).next, end, dist + map[start].get(i).dist);
            }
        }
    }
}

class Node {
    int next;
    int dist;

    public Node(int next, int dist) {
        this.next = next;
        this.dist = dist;
    }
}
```
