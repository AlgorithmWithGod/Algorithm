```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    static int len,maxRemoveCnt, ans;
    static int[] arr,minArr,maxArr;

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        len = Integer.parseInt(st.nextToken());
        maxRemoveCnt = Integer.parseInt(st.nextToken());
        arr = new int[len];
        ans = Integer.MIN_VALUE;
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < len; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

    }

    private static void process() {
        getMinAndMaxArr();
        for (int i = 0; i <= maxRemoveCnt; i++) {
            int end = (len-1) -  i;
            int start = maxRemoveCnt - i;

            ans = Math.max(maxArr[end] - arr[start], ans);
        }
    }

    private static void getMinAndMaxArr() {
        minArr = new int[len]; // 0~i번까지의 숫자중 최솟값
        maxArr = new int[len]; // len-1 ~ len-1-i번까지의 숫자 중 최댓값

        minArr[0] = arr[0];
        for (int i = 1; i < len; i++) {
            minArr[i] = Math.min(minArr[i-1], arr[i]);
        }
        maxArr[len-1] = arr[len-1];
        for (int i = len-2; i >= 0; i--) {
            maxArr[i] = Math.max(maxArr[i+1], arr[i]);
        }
    }

    private static void print()  {
        System.out.println(ans);
    }



}
```