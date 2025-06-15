```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,K;
    static int[][] jewelryInfo;
    static TreeMap<Integer,Integer> backpack; //중복되는 가방 구분을 위한 맵
    static long sum;


    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        jewelryInfo = new int[N][2]; // 0이면 무게, 1이면 가격
        backpack = new TreeMap<>();
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            jewelryInfo[i][0] = Integer.parseInt(st.nextToken());
            jewelryInfo[i][1] = Integer.parseInt(st.nextToken());
        }
        for (int i = 0; i < K; i++) {
            int capacity = Integer.parseInt(br.readLine());
            backpack.put(capacity,backpack.getOrDefault(capacity,0)+1);
        }
        Arrays.sort(jewelryInfo,(a,b) -> b[1]-a[1]);

        sum = 0;
        for (int i = 0; i < N; i++) {
            Integer cur = backpack.ceilingKey(jewelryInfo[i][0]);
            if(cur != null){
                sum += jewelryInfo[i][1];
                backpack.put(cur,backpack.get(cur)-1);
                if(backpack.get(cur)==0){
                    backpack.remove(cur);
                }
            }
        }
        bw.write(sum+"");
        bw.close();
    }
}
```
