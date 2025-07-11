```java
import java.util.*;
import java.io.*;

public class boj2262 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
        nextLine();
        int n = nextInt();
        nextLine();
        List<Integer> rank = new ArrayList<>();
        for (int i = 0; i < n; i++) rank.add(nextInt());
        int answer = 0;
        while (rank.size() > 1) {
            int max = -1;
            int idx = -1;

            for (int i = 0; i < rank.size(); i++) {
                if (rank.get(i) > max) {
                    max = rank.get(i);
                    idx = i;
                }
            }

            int diff;
            if (idx == 0) diff = Math.abs(rank.get(idx) - rank.get(idx + 1));
            else if (idx == rank.size() - 1) diff = Math.abs(rank.get(idx) - rank.get(idx - 1));
            else {
                int left = Math.abs(rank.get(idx) - rank.get(idx - 1));
                int right = Math.abs(rank.get(idx) - rank.get(idx + 1));
                diff = Math.min(left, right);
            }

            answer += diff;
            rank.remove(idx);
        }

        System.out.println(answer);
    }
}
```
