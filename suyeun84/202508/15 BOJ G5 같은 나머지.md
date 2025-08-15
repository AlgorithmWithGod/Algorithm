```java
import java.io.*;
import java.util.*;

public class boj1684 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}

	public static void main(String[] args) throws Exception {
		nextLine();
		int n = nextInt();
        int[] arr = new int[n];
        nextLine();
        for (int i = 0; i < n; i++) arr[i] = nextInt();
        Arrays.sort(arr);
        int min = arr[0];
        int i = 0;
        for (i = 0; i < n; i++) if ((arr[i] -= min) != 0) break;
        if (i == n) {
            System.out.println(min);
            return;
        }
        int gcd = arr[i++];
        for (; i < n; i++) gcd = gcd(gcd, arr[i]-=min);
        System.out.println(gcd);
	}

	static int gcd(int a, int b) {
        int r = -1;
        while (r!=0) {
            r = a % b;
            a = b;
            b = r;
        }
        return a;
    }
}
```
