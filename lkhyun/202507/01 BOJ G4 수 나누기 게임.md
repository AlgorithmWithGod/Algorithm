```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] playerCard;
    static int[] playerScore;
    static boolean[] exist;
    static HashMap<Integer,Integer> idx;

    public static void main(String[] args) throws Exception{
        N = Integer.parseInt(br.readLine());
        playerScore = new int[N+1];
        playerCard = new int[N+1];
        exist = new boolean[1000001];
        idx = new HashMap<>();
        st = new StringTokenizer(br.readLine());

        int max = 0;
        for (int i = 1; i <= N; i++) {
            playerCard[i] = Integer.parseInt(st.nextToken());
            exist[playerCard[i]] = true;
            idx.put(playerCard[i],i);
            max = Math.max(max, playerCard[i]);
        }

        for (int i = 1; i <= N; i++) {
            for(int j = playerCard[i]; j <= max; j+=playerCard[i]) {
                if(exist[j]){
                    playerScore[i]++;
                    playerScore[idx.get(j)]--;
                }
            }
        }
        StringBuffer sb = new StringBuffer();
        for (int i = 1; i <= N; i++) {
            sb.append(playerScore[i]).append(" ");
        }
        bw.write(sb.toString());
        bw.close();
    }
}
```
