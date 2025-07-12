```java
import java.util.*;
import java.io.*;

public class boj10282 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	static int INF = Integer.MAX_VALUE;
	
    static ArrayList<Computer>[] list;
    static int[] dist;
    static boolean[] visited;
	public static void main(String[] args) throws Exception {
		nextLine();
		int T = nextInt();
		
        for (int t = 0; t < T; t++) {
            nextLine();
			
            int n = nextInt();
            int d = nextInt();
            int c = nextInt();
			
            list = new ArrayList[n + 1];
            dist = new int[n + 1];
            visited = new boolean[n + 1];
		
            for (int i = 1; i < n + 1; i++) {
                dist[i] = INF;
                list[i] = new ArrayList<>();
            }
			
            for (int i = 0; i < d; i++) {
                nextLine();
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                int s = Integer.parseInt(st.nextToken());
				
                list[b].add(new Computer(a, s));
            }
			
            dijkstra(c);
			
            int infection = 0;
            int answer = 0;
			
            for (int i = 1; i < n + 1; i++) {
                if (dist[i] != INF) {
                    infection++;
                    answer = Math.max(answer, dist[i]);
                }
            }
            System.out.println(infection + " " + answer);
        }
    }
	
    public static void dijkstra(int start) {
        PriorityQueue<Computer> q = new PriorityQueue<>();
		
        dist[start] = 0;
        q.offer(new Computer(start, 0));
		
        while (!q.isEmpty()) {
            int cur = q.poll().depend;
			
            if (!visited[cur]) {
                visited[cur] = true;
				
                for (Computer next : list[cur]) {
                    if (dist[next.depend] > dist[cur] + next.time) {
                        dist[next.depend] = dist[cur] + next.time;
                        q.add(new Computer(next.depend, dist[next.depend]));
                    }
                }
            }
        }   
    }
}

class Computer implements Comparable<Computer> {
    int depend;
    int time;
	
    public Computer(int depend, int time) {
        this.depend = depend;
        this.time = time;
    }

    @Override
    public int compareTo(Computer o) {
        return this.time - o.time;
    }
}
```
