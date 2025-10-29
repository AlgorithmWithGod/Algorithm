```java
import java.io.*;
import java.util.*;

public class boj2056 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
    	nextLine();
    	int N = nextInt();
    	int[] time = new int[N+1];
    	int[] degree = new int[N + 1];
    	int answer = 0;
    	ArrayList<ArrayList<Integer>> work = new ArrayList<>();
    	for (int i = 0; i < N+1; i++) work.add(new ArrayList<>());
    	for (int i = 1; i <= N; i++) {
    		nextLine();
    		time[i] = nextInt();
    		int M = nextInt();
    		for (int j = 0; j < M; j++) {
    			int num = nextInt();
    			work.get(num).add(i);
    			degree[i]++;
    		}
    	}
    	// 위상 정렬
    	Queue<Integer> q = new LinkedList<>();
    	int[] result = new int[N + 1];
    	for (int i = 1; i <= N; i++) {
    		result[i] = time[i];
    		if (degree[i] == 0) q.add(i);
    	}
    	
    	while(!q.isEmpty()) {
    		int cur = q.poll();
    		for (int next : work.get(cur)) {
    			degree[next]--;
    			result[next] = Math.max(result[next], result[cur] + time[next]);
    			if (degree[next] == 0) q.add(next);
    		}
    	}
    	
    	for (int i = 0; i <= N; i++) answer = Math.max(answer,  result[i]);
    	System.out.println(answer);
    }
}
```
