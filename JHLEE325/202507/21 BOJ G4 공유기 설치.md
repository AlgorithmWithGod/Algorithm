```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {

    static int n, c;
    static int[] house;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        c = Integer.parseInt(st.nextToken());

        house = new int[n];
        for (int i = 0; i < n; i++) {
            house[i] = Integer.parseInt(br.readLine());
        }

        Arrays.sort(house);

        int low = 1;
        int high = house[n - 1] - house[0];
        int answer = 0;

        while (low <= high) {
            int mid = (low + high) / 2;

            if (canInstall(mid)) {
                answer = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        System.out.println(answer);
    }

    static boolean canInstall(int distance) {
        int count = 1;
        int lastInstalled = house[0];

        for (int i = 1; i < n; i++) {
            if (house[i] - lastInstalled >= distance) {
                count++;
                lastInstalled = house[i];
            }
        }

        return count >= c;
    }
}

```
