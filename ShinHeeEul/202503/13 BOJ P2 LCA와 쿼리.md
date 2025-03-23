```java
import java.io.*;
import java.util.*;

public class Main {

    
    static ArrayList<Integer>[] lists;
    
    static int[][] parents;
    static boolean[] visited;
    static int[] depths;
    static int logN;
    
    public static void main(String[] args) throws Exception {
        // TODO Auto-generated method stub
        
        int N = read();
        
        lists = new ArrayList[N + 1];
        visited = new boolean[N + 1];
        depths = new int[N + 1];
        logN = (int) (Math.log(N) / Math.log(2));
        parents = new int[N + 1][logN + 1];
        
        for(int i = 0; i <= N; i++) {
            lists[i] = new ArrayList<>();
        }
        
        // 트리 만들고       
        for(int i = 1; i < N; i++) {
            
            int a = read();
            int b = read();
            
            lists[a].add(b);
            lists[b].add(a);
        }

        visited = new boolean[N + 1];
        parents = new int[N + 1][logN + 1];
        
        // dfs
        dfs();
        
        // parents 배열 만들기
        for(int i = 1; i <= logN; i++) {
        	for(int j = 2; j <= N; j++) {
        		parents[j][i] = parents[parents[j][i-1]][i-1];
        	}
        }

        int M = read();
        StringBuilder sb = new StringBuilder();
        
        for(int i = 0; i < M; i++) {
        	
        	int r = read();
        	int u = read();
        	int v = read();
        	
        	// depths 높이 맞추기
        	
        	// lca 3번
        	int mr = lca(r, u);
        	int mu = lca(r, v);
        	int mv = lca(u, v);
        	
        	
        	int ans = mr;
        	if(depths[ans] < depths[mu]) {
        		ans = mu;
        	}
        	if(depths[ans] < depths[mv]) {
        		ans = mv;
        	}
        	sb.append(ans).append("\n");
        	
        }
        
        System.out.println(sb);
        
    }
    
    public static int lca(int a, int b) {
    	
    	int depthA = depths[a];
    	int depthB = depths[b];
    	

    	if(depthA < depthB) {
    		b = diff(b, depthB - depthA);
    	} else {
    		a = diff(a, depthA - depthB);
    	}

    	if(a == b) return a;
    	
    	
    	for(int i = logN; i >= 0; i--) {
    		
    		int aa = parents[a][i];
    		int bb = parents[b][i];
    		
    		if(aa == bb) continue;
    		
    		
    		a = aa;
    		b = bb;
    	}
    	
    	if(a == b) return a;
    	
    	return parents[a][0];
    }
    
    public static int diff(int a, int diff) {
    	
    	for(int i = 0; (1 << i) <= diff ; i++) {
    		int de = (1 << i);
    		
    		if((de | diff) == diff) {
    			a = parents[a][i];
    		}
    	}
    	
    	return a;
    }
    
    public static void dfs() {
        
        Stack<Node> stack = new Stack<>();
        stack.add(new Node(1, 1));
        visited[1] = true;
        while(!stack.isEmpty()) {
            Node node = stack.pop();
        	int val = node.val;
        	int depth = node.depth;
           depths[val] = depth;
            for(int nxt : lists[val]) {
            	if(visited[nxt]) continue;
            	visited[nxt] = true;
            	parents[nxt][0] = val;
            	
            	stack.add(new Node(nxt, depth + 1));
            }
            
        }
    }
    
    public static class Node implements Comparable<Node> {
    	int depth;
    	int val;
    	
    	Node(int val, int depth) {
    		this.depth = depth;
    		this.val = val;
    	}
    	
    	public int compareTo(Node o) {
    		return this.depth - o.depth;
    	}
    }

    private static int read() throws Exception {
        int d, o;
        d = System.in.read();


        o = d & 15;
        while ((d = System.in.read()) > 32)
            o = (o << 3) + (o << 1) + (d & 15);

        return o;
    }
    
    
}
```
