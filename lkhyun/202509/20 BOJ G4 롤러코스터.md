```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] tops;
    static int[] decrease;
    static int[] increase;
    
    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        tops = new int[N];
        decrease = new int[N];
        increase = new int[N];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            tops[i] = Integer.parseInt(st.nextToken());
        }

        for (int i = 0; i < N; i++) {
            decrease[i] = 1;
            for (int j = 0; j < i; j++) {
                if (tops[j] > tops[i] && decrease[i] < decrease[j] + 1) {
                    decrease[i] = decrease[j] + 1;
                }
            }
        }

        for (int i = N - 1; i >= 0; i--) {
            increase[i] = 1;
            for (int j = i + 1; j < N; j++) {
                if (tops[i] < tops[j] && increase[i] < increase[j] + 1) {
                    increase[i] = increase[j] + 1;
                }
            }
        }

        int maxLen = 0;
        for (int i = 0; i < N; i++) {
            maxLen = Math.max(maxLen, decrease[i] + increase[i] - 1);
        }

        bw.write(maxLen + "");
        bw.close();
    }
}
```
