```java
import java.io.*;
import java.util.*;

public class Main {
	
	
	static boolean[] visited;
	static int N;
	static ArrayList<Integer>[] lists;
	
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        long K = Long.parseLong(st.nextToken());
        
        visited = new boolean[N + 1];
        
        st = new StringTokenizer(br.readLine());
        
        PriorityQueue<Integer[]> pq = new PriorityQueue<>((o1, o2) -> o1[1] - o2[1]);

        
        lists = new ArrayList[N + 1];
        
        for(int i = 1; i <= N; i++) pq.add(new Integer[] {i, Integer.parseInt(st.nextToken())});
        for(int i = 1; i < N + 1; i++) lists[i] = new ArrayList<>();
        
        
        
        for(int i = 0; i < M; i++) {
        	st = new StringTokenizer(br.readLine());
            
        	int a = Integer.parseInt(st.nextToken());
        	int b = Integer.parseInt(st.nextToken());
        	
        	lists[a].add(b);
        	lists[b].add(a);
        	
        }
        
        if(M <= 1) {
        	System.out.println("YES");
        	return;
        }
        
        while(!pq.isEmpty()) {
        	Integer[] node = pq.poll();
        	int current = node[0];
        	if(visited[current]) continue;
        	K -= node[1];
        	
        	if(K < 0L) break;
        	
        	visited[current] = true;
        	backTracking(current);
        }
        
        System.out.println(K >= 0L ? "YES" : "NO");
        
    }
    
    public static void backTracking(int current) {
    	
    	
    	int next = current + 1;
    	if(next == N + 1) next = 1;
    	int next2 = current - 1;
    	if(next2 == 0) next2 = N;
    	
    	if(!visited[next] && !lists[current].contains(next)) {
    		visited[next] = true;
    		backTracking(next);
    	}
    	if(!visited[next2] && !lists[current].contains(next2)) {
    		visited[next2] = true;
    		backTracking(next2);
    	}
    }

}
```
