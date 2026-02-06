```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Main{
	private static long[] Times;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] tokens = br.readLine().split(" ");
		int n = Integer.parseInt(tokens[0]);
		long m = Long.parseLong(tokens[1]);
		Times = new long[n];
		for(int i = 0; i < n; i++){
			Times[i] = Integer.parseInt(br.readLine());
		}
		Arrays.sort(Times);
		long l = Times[0] -1; // check(l) == false
		long r = Times[Times.length-1] * m + 1; // check(r) == true
		while(l + 1< r){
			long mid = (l + r) / 2;
			// System.out.println("%d %d %d".formatted(l, r, mid));
			if(check(mid, m)){
				r = mid;
			}else
				l = mid;
		}
		System.out.println(r);
		br.close();
	}

	private static boolean check(long width, long m) {
		long block = 0;
		for(long t : Times){
			block += width / t;
			if(block >= m)
				return true;
		}
		return (block >= m);
	}
}
```
