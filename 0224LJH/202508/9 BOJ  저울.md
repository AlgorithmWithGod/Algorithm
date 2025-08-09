```java
import java.awt.*;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;
import java.util.List;


public class Main {

    static int size,ans;
    static int[] arr;



    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        size = Integer.parseInt(br.readLine());
        arr = new int[size];
        ans = 0;
        StringTokenizer st = new StringTokenizer(br.readLine());

        for (int i = 0; i < size; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }


    }

    private static void process() throws IOException {
        Arrays.sort(arr);

        if ( arr[0] != 1) return;
        ans = 1;

        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > ans +1) {
                return;
            }
            ans += arr[i];

        }



    }


    private static void print() {
        System.out.println(ans+1);
    }
}
```