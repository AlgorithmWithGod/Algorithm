```java
import java.io.*;
import java.util.*;

public class boj1034 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int M = nextInt();
		int answer = 0;
		String[] input = new String[N];
		for (int i = 0; i < N; i++) input[i] = br.readLine();
		HashMap<String, Integer> map = new HashMap<>();
        int K = Integer.parseInt(br.readLine());
        for (int i = 0; i < N; i++) {
            int count = 0;
            for (int j = 0; j < M; j++) {
                if (input[i].charAt(j) == '0') {
                    count++;
                }
            }
            if (count <= K && count % 2 == K % 2) {
                map.put(input[i], map.getOrDefault(input[i], 0) + 1);
                if (map.get(input[i]) > answer) {
                    answer = map.get(input[i]);
                }
            }
        }
        System.out.println(answer);
	}
}
```
