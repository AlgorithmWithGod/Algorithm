```java
import java.io.*;
import java.math.BigInteger;
import java.util.*;

public class Main {
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        BigInteger moves = BigInteger.ONE.shiftLeft(N).subtract(BigInteger.ONE);
        sb.append(moves).append("\n");

        if (N <= 20) {
            hanoi(N, 1, 3, 2);
        }

        System.out.println(sb.toString());
    }

    static void hanoi(int n, int from, int to, int temp) {
        if (n == 1) {
            sb.append(from).append(" ").append(to).append("\n");
            return;
        }
        hanoi(n - 1, from, temp, to);
        sb.append(from).append(" ").append(to).append("\n");
        hanoi(n - 1, temp, to, from);
    }
}
```
