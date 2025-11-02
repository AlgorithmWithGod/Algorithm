```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        double agoal = Double.parseDouble(br.readLine().trim()) / 100.0;
        double bgoal = Double.parseDouble(br.readLine().trim()) / 100.0;

        boolean[] isPrime = new boolean[18+1];
        int[] primes = {2, 3, 5, 7, 11, 13, 17};
        for (int p : primes) isPrime[p] = true;

        double nonPrimeA = 0.0;
        for (int a = 0; a <= 18; a++) {
            if (!isPrime[a]) {
                nonPrimeA += comb(18, a) * Math.pow(agoal, a) * Math.pow(1 - agoal, 18 - a);
            }
        }

        double nonPrimeB = 0.0;
        for (int b = 0; b <= 18; b++) {
            if (!isPrime[b]) {
                nonPrimeB += comb(18, b) * Math.pow(bgoal, b) * Math.pow(1 - bgoal, 18 - b);
            }
        }

        double no = nonPrimeA * nonPrimeB;

        double result = 1.0 - no;

        System.out.printf("%.6f\n", result);
    }

    static double comb(int n, int k) {
        if (k > n) return 0;
        if (k > n - k) k = n - k;
        double res = 1.0;
        for (int i = 0; i < k; i++) {
            res *= (n - i);
            res /= (i + 1);
        }
        return res;
    }
}
```
