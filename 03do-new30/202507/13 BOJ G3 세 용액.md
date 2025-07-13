```java
import java.io.*;
import java.util.*;

public class Main {
    static int N;
    static long[] arr, answer;
    static long minAbs;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        arr = new long[N];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Long.parseLong(st.nextToken());
        }
        Arrays.sort(arr);
        minAbs = 3_000_000_000L;
        for (int startIdx = 0; startIdx < N-2; startIdx++) {
            twoPointer(startIdx);
        }
        for (long num : answer) {
            System.out.print(num + " ");
        }
        br.close();
    }

    private static void twoPointer(int startIdx) {
        int leftIdx = startIdx + 1;
        int rightIdx = N-1;
        while (leftIdx < rightIdx) {
            long currentVal = arr[startIdx] + arr[leftIdx] + arr[rightIdx];
            long currentAbs = Math.abs(currentVal);
            if (currentAbs < minAbs) {
                minAbs = currentAbs;
                answer = new long[] {arr[startIdx], arr[leftIdx], arr[rightIdx]};
            }
            if (currentVal < 0) {
                leftIdx++;
            } else if (currentVal > 0) {
                rightIdx--;
            } else {
                break;
            }
        }
    }
}

```
