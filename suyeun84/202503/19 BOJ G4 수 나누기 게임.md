```java
import java.io.*;
import java.util.*;

public class boj27172 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}
    
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		nextLine();
		int[] card = new int[N];
		int[] selected = new int[1000001];
		int[] answer = new int[N+1];
		for (int i = 0; i < N; i++) {
			card[i] = nextInt();
			selected[card[i]] = i+1;
		}
		
		for (int i = 0; i < N; i++) {
			int start = card[i];
			for (int j = start*2; j < 1000001; j += start) {
				if (selected[j] > 0) {
					answer[selected[j]] -= 1;
					answer[selected[start]] += 1;
				}
			}
		}
		for (int i = 1; i < N+1; i++) {
			System.out.print(answer[i]+" ");
		}
	}
}
```
