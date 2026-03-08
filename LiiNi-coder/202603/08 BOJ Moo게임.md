```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main{
	private static long[] Arr = new long[50];
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		long N = Long.parseLong(br.readLine());
		Arr[0] = 3;
		int k = 0;

		while(Arr[k]<N){
			k++;
			Arr[k] = Arr[k-1]*2 + (k+3);
		}
		System.out.println(find(k,N));
	}

	private static char find(int k,long n){
		if(k==0){
			if(n==1)
				return 'm';
			return 'o';
		}

		if(n<= Arr[k-1]){
			return find(k-1,n);
		}

		if(n> Arr[k-1] && n<= Arr[k-1]+k+3){
			if(n== Arr[k-1] + 1)
				return 'm';
			return 'o';
		}

		return find(k-1,n - (Arr[k-1]+ (k+3)));
	}
}
```
