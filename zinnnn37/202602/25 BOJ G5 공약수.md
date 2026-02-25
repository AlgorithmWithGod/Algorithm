```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_2436_공약수 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int gcd, lcm;
    private static long resA, resB;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        gcd = Integer.parseInt(st.nextToken());
        lcm = Integer.parseInt(st.nextToken());
    }

    private static void sol() throws IOException {
        long div = lcm / gcd;

        for (int i = 1; i <= Math.sqrt(div); i++) {
            if (div % i == 0) {
                long a = i;
                long b = div / i;

                if (gcd(a, b) == 1) {
                    resA = a;
                    resB = b;
                }
            }
        }
        bw.write((resA * gcd) + " " + (resB * gcd));
        bw.flush();
        bw.close();
        br.close();
    }

    private static long gcd(long a, long b) {
        while (b != 0) {
            long tmp = b;
            b = a % b;
            a = tmp;
        }

        return a;
    }

}
```