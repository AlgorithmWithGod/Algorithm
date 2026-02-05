```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.HashSet;
import java.util.Map;
import java.util.Set;

public class Main{
	private static int N = 0;
	private static int H = 0;
	private static int[][] Arrs = null;
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] tokens = br.readLine().split(" ");
		N = Integer.parseInt(tokens[0]) / 2;
		H = Integer.parseInt(tokens[1]);
		Arrs = new int[2][N];

		int N2 = N * 2;
		for(int i = 0; i < N2; i++){
			int v = Integer.parseInt(br.readLine());
			if(i % 2 == 0)
				Arrs[0][i / 2] = v;
			else
				Arrs[1][i/2] = v;
		}
		Arrays.sort(Arrs[0]);
		Arrays.sort(Arrs[1]);
		int[] result = new int[H + 1];
		int minV = 200_001;
		for(int h = 1; h <= H; h++){
			int r1 = N - lowerBound(Arrs[0], h);
			int r2 = N - lowerBound(Arrs[1], H - h + 1);
			result[h] = r1 + r2;
			minV = Math.min(minV, result[h]);
		}
		int countMinV = 0;
		for(int h = 1; h <= H;h++){
			if(minV == result[h])
				countMinV++;
		}
		System.out.println(minV + " " + countMinV);
		br.close();
	}

	private static int lowerBound(int[] arr, int v) {
		int l = -1; int r = arr.length;
		while(l + 1 < r){
			int mid = (l + r) / 2;
			if(arr[mid] >= v){ // check(lo)== false;
				//check(mid) == true
				r = mid;
			}else{
				l = mid;
			}
		}
		return r;
	}
}
```
