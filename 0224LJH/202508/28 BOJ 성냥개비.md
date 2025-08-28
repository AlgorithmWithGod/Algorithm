```java
import java.io.IOException;
import java.math.BigInteger;
import java.io.*;
import java.util.*;


public class Main {
	
	// 1-> 2개 | 2 -> 5개 | 3 -> 5개 | 4개 -> 4개 | 5 -> 5개 | 
	// 6-> 6개 | 7 -> 3개 | 8 -> 7개 | 9개 -> 6개 | 0 -> 6개 |
	
	static int[] costs = {6 , 2, 5, 5, 4, 5, 6, 3, 7, 6, 6};
	static BigInteger[] max, min;
	
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static int cnt = 0;
	static final int LARGER = 1;
	static final int SMALLER = -1;
	
	public static void main(String[] args) throws IOException {
		int TC = Integer.parseInt(br.readLine());
		
		for (int tc = 1; tc <= TC; tc++) {
			init();
			process();
			print();
		}
	}
	
	public static void init() throws IOException {
		cnt = Integer.parseInt(br.readLine());
		max = new BigInteger[cnt+1];
		min = new BigInteger[cnt+1];
		
		for (int i = 0; i <= cnt; i++) max[i] = BigInteger.ZERO;
		min[0] = BigInteger.ZERO;
	}
	
	public static void process() throws IOException {
		for (int i = 0; i < cnt; i++) {
			BigInteger lNum = max[i];
			BigInteger sNum = min[i];
			
			
			int left = cnt - i;
			for (int j = 0; j < 10; j++) {
				if (left < costs[j]) continue;
				
				BigInteger plus = BigInteger.valueOf(j); 
				BigInteger nLNum = lNum.multiply(BigInteger.valueOf(10)).add(plus);
				
				
				if ( nLNum.compareTo( max[i+costs[j]]) == LARGER) max[i+costs[j]] = nLNum;
			}
			
			if (sNum == null) continue;
			
			
			for (int j = 0; j < 10; j++) {
				

				if (sNum == BigInteger.ZERO && j == 0) continue;
				if (left < costs[j]) continue;
				
				BigInteger plus = BigInteger.valueOf(j); 
				BigInteger nSNum = sNum.multiply(BigInteger.valueOf(10)).add(plus);
				
				if (min[i+costs[j]] == null
						|| nSNum.compareTo(min[i+costs[j]]) == SMALLER) min[i+costs[j]] = nSNum;
				
			}
		}

	}

	

	public static void print() {
		System.out.println(min[cnt].toString() + " " +  max[cnt].toString());
	}
}

```
