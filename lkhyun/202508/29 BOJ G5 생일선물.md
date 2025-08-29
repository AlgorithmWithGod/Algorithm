```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,D;
    static class present{
        int price,value;

        present(int price, int value){
            this.price = price;
            this.value = value;
        }
    }
    static present[] arr;

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        D = Integer.parseInt(st.nextToken());
        arr = new present[N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            arr[i] = new present(Integer.parseInt(st.nextToken()),Integer.parseInt(st.nextToken()));
        }
        Arrays.sort(arr,(a,b) -> Integer.compare(a.price,b.price));
        long cur = 0,max = 0;
        int left = 0,right = 0;
        while(right < N){
            if(arr[right].price - arr[left].price < D){
                cur += arr[right++].value;
                max = Math.max(max,cur);
            }else{
                cur -= arr[left++].value;
            }
        }
        bw.write(max+"");
        bw.close();
    }
}
```
