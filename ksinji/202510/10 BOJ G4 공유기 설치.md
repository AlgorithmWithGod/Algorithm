```java
import java.io.*;
import java.util.*;

public class Main {
    static int N, C;
    static int[] house;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());

        house = new int[N];
        for (int i = 0; i < N; i++) house[i] = Integer.parseInt(br.readLine());
        Arrays.sort(house);

        int lo = 1; // 최소 간격
        int hi = house[N - 1] - house[0]; // 최대 간격
        int ans = 0;

        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (canPlace(mid)) { // mid 간격으로 C개 설치 가능
                ans = mid;
                lo = mid + 1;
            } else {
                hi = mid - 1;
            }
        }

        System.out.println(ans);
    }

    // dist 간격을 유지하며 C개 설치 가능한지
    static boolean canPlace(int dist) {
        int count = 1; // 첫 집에 설치
        int last = house[0];
        for (int i = 1; i < N; i++) {
            if (house[i] - last >= dist) {
                count++;
                last = house[i];
                if (count >= C) return true;
            }
        }
        return false;
    }
}
```
