```java
import java.io.*;
import java.math.BigInteger;

public class Main {

	static int MAX_IDX = 20; // 2의 20승이 1,000,000과 가장 가까움

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

		int N = Integer.parseInt(br.readLine());
		int[][] arr = new int[N][MAX_IDX]; // N번째 숫자 이진수로 변환한 결과를 담는다. arr[i][j] = i번째 숫자의 j번째 비트

		for (int i = 0; i < N; i++) {
			String binary = Integer.toBinaryString(Integer.parseInt(br.readLine()));
			// binary 문자열의 인덱스 역순으로 arr[i]에 담아준다.
			int binaryLength = binary.length();
			for (int j = 0; j < binaryLength; j++) {
				arr[i][j] = binary.charAt(binaryLength - j - 1) - '0';
			}
		}

		BigInteger answer = BigInteger.ZERO;
		// 2^j + (j열에 있는 모든 1의 개수 * j열에 있는 모든 0의 개수)
		for (int j = 0; j < MAX_IDX; j++) {
			// j열에 있는 모든 1의 개수
			int cntOne = 0;
			// j열에 있는 모든 0의 개수
			int cntZero = 0;
			for (int i = 0; i < N; i++) {
				if (arr[i][j] == 1) {
					cntOne++;
				} else {
					cntZero++;
				}
			}
			BigInteger tmp1 = BigInteger.valueOf((long) Math.pow(2, j));
			BigInteger tmp2 = BigInteger.valueOf((long) cntOne * cntZero);
			BigInteger result = tmp1.multiply(tmp2);
			answer = answer.add(result);
		}

		bw.write(answer + "\n");

		br.close();
		bw.flush();
		bw.close();
	}
}
```
