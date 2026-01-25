```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int N = Integer.parseInt(br.readLine());

        int[] P = new int[N];
        int[] S = new int[N];
        int[] cards = new int[N];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) P[i] = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) S[i] = Integer.parseInt(st.nextToken());

        for (int i = 0; i < N; i++) cards[i] = i;

        int[] initial = cards.clone();
        int count = 0;

        while (true) {
            if (isTarget(cards, P)) {
                System.out.println(count);
                break;
            }

            int[] nextCards = new int[N];
            for (int i = 0; i < N; i++) {
                nextCards[S[i]] = cards[i];
            }
            cards = nextCards;
            count++;

            if (Arrays.equals(cards, initial)) {
                System.out.println("-1");
                break;
            }
        }
    }

    private static boolean isTarget(int[] cards, int[] P) {
        for (int i = 0; i < cards.length; i++) {
            if (P[cards[i]] != i % 3) {
                return false;
            }
        }
        return true;
    }
}
```
