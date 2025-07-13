```java
import java.util.*;
import java.io.*;

public class Main {
    static int N, answer;
    static long[] arr;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        arr = new long[N];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Long.parseLong(st.nextToken());
        }
        Arrays.sort(arr);
        answer = 0;
        for (int i = 0; i < N; i++) {
            twoPointer(i);
        }
        System.out.println(answer);

        br.close();
    }
    private static void twoPointer(int targetIdx) {
        long target = arr[targetIdx];
        int leftIdx = 0;
        int rightIdx = N-1;
        while (leftIdx < rightIdx) {
            long sum = arr[leftIdx] + arr[rightIdx];
            if (target == sum) {
                if (leftIdx == targetIdx) {
                    leftIdx++;
                } else if (rightIdx == targetIdx) {
                    rightIdx--;
                } else {
                    answer++;
                    return;
                }
            }
            else if (sum < target) {
                leftIdx++;
            } else {
                rightIdx--;
            }
        }
    }

}
```
