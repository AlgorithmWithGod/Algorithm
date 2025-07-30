```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
    static int[] arr,lis,lds;
    static int len,ans;


    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        len = Integer.parseInt(br.readLine());
        arr = new int[len];
        lis = new int[len];
        lds = new int[len];
        ans = 0;

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < len; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
    }

    private static void process() throws IOException {
        Arrays.fill(lis, 1);
        Arrays.fill(lds, 1);

        for (int i = 1; i < len; i++) {
            for (int j = 0; j < i; j++){
                if (arr[i] > arr[j]) lis[i] = Math.max(lis[i], lis[j] + 1);
            }
        }

        for (int i = len -1; i >= 0; i--) {
            for (int j = len-1; j > i; j--){
                if (arr[i] > arr[j]) lds[i] = Math.max(lds[i], lds[j] + 1);
            }
        }

        for (int i = 0; i < len; i++){
            ans = Math.max(ans, lis[i] + lds[i] - 1);
        }
    }

    private static void print() {
        System.out.println(ans);
    }
}
```