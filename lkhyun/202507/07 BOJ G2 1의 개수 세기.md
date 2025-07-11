```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    public static void main(String[] args) throws Exception{
        st = new StringTokenizer(br.readLine());
        long A = Long.parseLong(st.nextToken());
        long B = Long.parseLong(st.nextToken());
        long total = countOnes(B) - countOnes(A-1);
        bw.write(String.valueOf(total));
        bw.close();
    }
    public static long countOnes(long N) {
        long result = 0;

        // 첫번째 비트: 0,1,0,1,0,1,0,1 -> 주기 2
        // 두번째 비트: 0,0,1,1,0,0,1,1 -> 주기 4
        // 세번째 비트: 0,0,0,0,1,1,1,1 -> 주기 8
        // ...
        for (int i = 0; i < 60; i++) {
            long bitPosition = 1L << i; // 한 주기에 있는 1의 개수

            long cycle = 2L * bitPosition; // 주기 구하기, 규칙을 보면 주기의 앞쪽 반절은 0, 뒤쪽 반절은 1임.

            long cycles = (N + 1) / cycle; //0부터 N까지 cycle 개수, 0부터니까 N+1로 구하기

            result += cycles * bitPosition; // 주기 x 한 주기에 있는 1의 개수 = 총 1의 개수

            long remainder = (N + 1) % cycle; // 나머지 구하기
            if (remainder > bitPosition) { // 나머지가 주기의 반절보다 크면 넘어선 만큼 더 더해줌.
                result += remainder - bitPosition;
            }
        }

        return result;
    }
}
```
