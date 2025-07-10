# 첫풀이 (hashSet이용)
## 코드
```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.HashSet;
import java.util.StringTokenizer;

public class Main {
	private static BufferedReader br;
	private static StringTokenizer st;
	private static BufferedWriter bw;

	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		bw = new BufferedWriter(new OutputStreamWriter(System.out));
		String line = br.readLine();
		st = new StringTokenizer(line);
		
		var sh = new HashSet<Integer>();
		while(st.hasMoreElements()){
			int ni = Integer.parseInt(st.nextToken());
			if(!sh.contains(ni)) {
				
				bw.write(ni + " ");
				sh.add(ni);
			}	
		}
		
		
		bw.flush();
		br.close();
		bw.close();
	}
}
```
## 결과
맞았습니다!!	396560KB	2260ms	Java 11
# 두번째 풀이(상태값bit집합이용)
## 코드
```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.HashSet;
import java.util.StringTokenizer;

public class Main {
	private static BufferedReader br;
	private static StringTokenizer st;
	private static BufferedWriter bw;

	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		bw = new BufferedWriter(new OutputStreamWriter(System.out));
		String line = br.readLine();
		st = new StringTokenizer(line);

		// 2^25개의 숫자가 등장하였는지 여부를 저장하는데에, int하나는 32개의 숫자를 검사 가능하니, 2^25 / 32 하여서 2^20개의 int필요
		int[] isAppeardNumber = new int[1<<20];
		
		while(st.hasMoreElements()){
			int ni = Integer.parseInt(st.nextToken());
			// isAppeardNumber 에 해당 숫자가 존재하면 == isAppeardNumber의 해당 bit가 1이라면
			int byte_index = ni/32;
			int bit_index = ni%32;
			if((isAppeardNumber[byte_index] & (1 << (bit_index))) == 0) {
				bw.write(ni + " ");
				// isAppeardNumber에 반영
				isAppeardNumber[byte_index] |= (1 << (bit_index));
			}	
		}
		
		
		bw.flush();
		br.close();
		bw.close();
	}
}
```
## 결과
맞았습니다!!	332500KB	1244ms	Java 11
