```java
import java.io.*;
import java.math.BigInteger;

public class Main {
    static int N;
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());

        BigInteger moves = BigInteger.valueOf(2).pow(N).subtract(BigInteger.ONE);
        sb.append(moves).append('\n');

        if (N <= 20) {
            hanoi(N, 1, 3, 2);
        }

        System.out.print(sb.toString());
    }

    // N개를 from -> to
    static void hanoi(int N, int from, int to, int temp) {
        if (N == 0) return;
        hanoi(N - 1, from, temp, to); // N-1개를 출발 -> 보조 기둥으로 옮김
        sb.append(from).append(' ').append(to).append('\n'); // 출발 -> 목적 기둥으로 남은 원판(젤 큰 거) 옮김
        hanoi(N - 1, temp, to, from); // N-1개를 보조 -> 목적 기둥으로 옮김
    }
}
```
