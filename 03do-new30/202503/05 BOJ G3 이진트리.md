```java
import java.util.*;

public class Main {
    static int K;
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        long N = sc.nextLong();
        K = sc.nextInt();
        int Q = sc.nextInt();
        for (int i = 0; i < Q; i++) {
            long x = sc.nextLong() - 1;
            long y = sc.nextLong() - 1;
            if (K == 1) {
                System.out.println(Math.abs(x - y));
            } else {
                int dist = 0;
                while (x != y) {
                    if (x < y) {
                        y = (y - 1) / K; // y = y의 부모 노드
                    } else {
                        x = (x - 1) / K; // x = x의 부모 노드
                    }
                    dist++;
                }
                System.out.println(dist);
            }
        }
        sc.close();
    }
}

```
