```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static long min,max;
    static List<Long> squares;
    static long cnt;
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        min = Long.parseLong(st.nextToken());
        max = Long.parseLong(st.nextToken());
        squares = new ArrayList<>();
        cnt = max-min+1;

        long temp = 2;
        while(temp*temp<=max){ //제곱수 저장
            squares.add(temp*temp);
            temp++;
        }

        Set<Long> s = new HashSet<>();

        for (long cur : squares) {
            long init = min/cur;
            long result = cur*init++;
            if(min%cur == 0) s.add(result);
            result = cur*init;
            while(result<=max){
                s.add(result);
                result = ++init * cur;
            }
        }

        bw.write((cnt - s.size())+"");
        bw.close();
    }

}
```
