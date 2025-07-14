 ```java
import java.util.*;
import java.io.*;

public class boj1038 {
    static List<Long> arr = new ArrayList<>();

    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        if(N <= 10) System.out.println(N);
        else{
            for(int i = 0; i < 10; i++) set(i, 1);
            if(N >= arr.size()) System.out.println(-1);
            else{
                Collections.sort(arr);
                System.out.println(arr.get(N));
            }
        }
    }

    static void set(long num, int val){
        if(val > 10) return;
        arr.add(num);
        for(int i = 0; i < num % 10; i++){
            set((num * 10) + i, val + 1);
        }
    }
}
```
