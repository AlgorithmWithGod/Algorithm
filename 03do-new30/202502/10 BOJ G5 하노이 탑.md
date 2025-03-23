```java
import java.io.*;
import java.math.BigInteger;
import java.util.*;

class Main {
	
	private static int N;
	private static StringBuilder sb;
	
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		
		N = Integer.parseInt(br.readLine());
		sb = new StringBuilder();
		
		BigInteger bigTwo = new BigInteger("2");
		
		// bw.flush()를 생략하면 틀리는 이유?
		// N=20일때, 아래 스트링빌더에 쓴 것도 같이출력해줘야 해서 bad -> flush를 해주면 통과하는구나
		bw.write(bigTwo.pow(N).subtract(BigInteger.ONE) + "\n");
		bw.flush();
//		System.out.println(bigTwo.pow(N).subtract(BigInteger.ONE));
		if (N <= 20) {
			hanoi(N, 1, 3);
			bw.write(sb + "");
		}
		
		br.close();
		bw.flush();
		bw.close();
	}
	
	private static void hanoi(int disks, int start, int end) {
		if (disks == 1) {
			sb.append(start + " " + end + "\n");
			return;
		}
		int via = 6 - start - end; // 경유지
		hanoi(disks-1, start, via);
		hanoi(1, start, end);
		hanoi(disks-1, via, end);
	}
}

```

- BigInteger
- BufferedWriter 사용 시 주의
