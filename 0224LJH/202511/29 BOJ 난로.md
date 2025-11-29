```java
import java.io.*;
import java.util.*;

public class Main {

	
	static int len, blockCnt;
	static long total;
	static long[] arr,diff;
			
	public static void main (String[] args) throws NumberFormatException, IOException {
		init();
		process();
		print();



	}
	
	public static void init() throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		len = Integer.parseInt(st.nextToken());
		blockCnt = Integer.parseInt(st.nextToken());
		arr = new long[len];
		total = 1;
		for (int i = 0; i < len; i++) {
			arr[i] = Long.parseLong(br.readLine());
		}

	}
	
	public static void process() {
		PriorityQueue<Long> q = new PriorityQueue<>(Collections.reverseOrder());
		for (int i = 0; i < len-1; i++) {
			q.add(arr[i+1]-arr[i]);
		}
		
		for (int i = 0; i < len-1; i++) {
			long cost = q.poll();
			if (i < blockCnt -1) cost =1;
			total += cost;
		}

	}
	

	
	public static void print() {
		System.out.println(total);
	}

}

```
