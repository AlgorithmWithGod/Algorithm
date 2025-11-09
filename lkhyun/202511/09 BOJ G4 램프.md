```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringBuilder sb = new StringBuilder();
    static StringTokenizer st;
    static int N,M,K;
    static Map<String, Integer> patterns = new HashMap<>();
    static int max = 0;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        for(int i = 0;i<N;i++){
            String input = br.readLine();
            patterns.put(input, patterns.getOrDefault(input, 0)+1);
        }
        K = Integer.parseInt(br.readLine());

        for(String s : patterns.keySet()){
            int zeroCnt = 0;
            for(int i = 0; i<s.length(); i++){
                if(s.charAt(i) == '0'){
                    zeroCnt++;
                }
            }
            if(zeroCnt <= K && (K-zeroCnt)%2 == 0){
                max = Math.max(max,patterns.get(s));
            }
        }
        bw.write(max+"");
        bw.close();
    }
}
```
