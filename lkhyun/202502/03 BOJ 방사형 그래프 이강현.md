```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.*;
public class Main {
    static BufferedReader br;
    static BufferedWriter bw;
    static int[] comb = new int[8];
    static boolean[] visited = new boolean[8];
    static int[] points = new int[8];
    static int count = 0;
    public static void main(String[] args) throws Exception {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st = new StringTokenizer(br.readLine());
        for(int i=0;i<8;i++){
            points[i] = Integer.parseInt(st.nextToken());
        }
        combination(0);
        bw.write(count+"");
        bw.flush();
    }
    public static void combination(int depth){
        if(depth==8){
            for(int i=0;i<8;i++){
                if(omok(i)){return;}
            }
            count++;
            return;
        }

        for(int j=0;j<8;j++){
            if(visited[j]){continue;}
            visited[j] = true;
            comb[depth] = points[j];
            combination(depth+1);
            visited[j] = false;
        }
    }
    public static boolean omok(int curpoint){
        double prev = (double)comb[(curpoint+7)%8];
        double next = (double)comb[(curpoint+1)%8];
        double slope = prev/next + 1;
        double distance = (prev / slope) * Math.sqrt(2);
        if(comb[curpoint] < distance){return true;}
        return false;
    }
}
```
