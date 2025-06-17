```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M,K;
    static HashSet<Integer> chosen;
    static int cheolyoung;
    static int answer = 0;

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        chosen = new HashSet<>();

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            chosen.add(Integer.parseInt(st.nextToken()));
            chosen.add(Integer.parseInt(st.nextToken()));
        }
        st = new StringTokenizer(br.readLine());
        int a = Integer.parseInt(st.nextToken());
        int b = Integer.parseInt(st.nextToken());
        cheolyoung = Math.abs(a%K - b%K);

        List<Integer> remainders = new ArrayList<>();
        for (int i = 1; i <= 4*N; i++) {
            if(!chosen.contains(i) && i != a && i != b) {
                remainders.add(i % K);
            }
        }
        Collections.sort(remainders);

        int size = remainders.size();
        int mid = size / 2;
        int left = 0;
        int right = mid;

        while (left < mid && right < size) {
            int diff = remainders.get(right) - remainders.get(left);

            if (diff > cheolyoung) {
                answer++;
                left++;
                right++;
            } else {
                right++;
            }
        }

        bw.write(Math.min(answer, M - 1) + "\n");
        bw.close();
    }
}
```
