```java
import java.io.*;
import java.util.*;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		int N = Integer.parseInt(st.nextToken());
		int L = Integer.parseInt(st.nextToken());

		int[][] sections = new int[N][2];
		for(int i = 0; i < N; i++){
			st = new StringTokenizer(br.readLine());
			sections[i][0] = Integer.parseInt(st.nextToken());
			sections[i][1] = Integer.parseInt(st.nextToken());
		}
		Arrays.sort(sections, (a, b) -> a[0] - b[0]);
		int coveredEnd = 0;
		int answer = 0;

		for(int i = 0; i < N; i++){
			int start = sections[i][0];
			int end = sections[i][1];
			if(coveredEnd >= end){
				continue;
			}

			int realStart = Math.max(coveredEnd, start);
			int remain = end - realStart;
			int count = remain / L;
			if(remain % L != 0){
				count++;
			}
			answer += count;
			coveredEnd = realStart + count * L;
		}

		System.out.println(answer);
	}
}

```
