```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;
import java.util.StringTokenizer;


public class Main {

	static int numCnt,ans;
	static int[] arr;
	static HashMap<Integer,HashSet<Integer>> good;
	
	public static void main(String[] args) throws IOException {
		init();
		process();
		print();
	}
	
	public static void init() throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		good = new HashMap<>();
		
		numCnt = Integer.parseInt(br.readLine());
		arr =new int[numCnt];
		ans = 0;
		
		StringTokenizer st = new StringTokenizer(br.readLine());
		for (int i = 0; i < numCnt; i++) {
			arr[i] = Integer.parseInt(st.nextToken());
		}
	}
	
	public static void process() throws IOException {
		for (int i = 0; i <numCnt; i++) {
			if (good.containsKey(arr[i])) {
				good.get(arr[i]).add(i);
			} else {
				good.put(arr[i], new HashSet<>());
				good.get(arr[i]).add(i);
			}
		}
		
		
		for (int i = 0; i < numCnt; i++) {
			for (int j = i+1; j < numCnt; j++){
				int sum = arr[i] + arr[j];
				
				if (!good.containsKey(sum)) continue;
				
				HashSet<Integer> idx = good.get(sum);
				
				boolean isRemovable = false;
				
				for (int n: idx) {
					if (n != i && n != j) {
						isRemovable = true;
						break;
					}
				}
				
				if (isRemovable) good.remove(sum);
				
			}
		}
		
		int zeroCnt = 0;
		for (int i = 0; i < numCnt; i++) if(arr[i] == 0) zeroCnt++;
		if (zeroCnt >= 3) good.remove(0);
		
		for (int i = 0; i < numCnt; i++) {
			if (!good.containsKey(arr[i])) ans++;
		}
		
	}

	

	public static void print() {
		System.out.println(ans);
	}
}

```
