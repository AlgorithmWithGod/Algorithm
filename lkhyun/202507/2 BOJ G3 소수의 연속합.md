```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static List<Integer> primes = new ArrayList<>();

    public static void main(String[] args) throws Exception{
        N = Integer.parseInt(br.readLine());
        if(N == 1){
            bw.write("0");
            bw.close();
            return;
        }

        loop: for (int i = 2; i <= N; i++) {
            for (int j = 2; j*j <= i; j++) {
                if(i%j == 0){
                    continue loop;
                }
            }
            primes.add(i);
        }
        int ans = 0;
        int left = 0;
        int sum = 0;
        for (int right = left; right < primes.size(); right++) {
            sum += primes.get(right);

            while(sum > N && left <= right){
                sum -= primes.get(left++);
            }

            if(sum == N){
                ans++;
            }
        }
        bw.write(ans +"");
        bw.close();
    }
}
```
