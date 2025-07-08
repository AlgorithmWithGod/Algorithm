```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static int G,P;
    static int[] nextBlank;
    static int count = 0;
    public static void main(String[] args) throws Exception{
        G = Integer.parseInt(br.readLine());
        P = Integer.parseInt(br.readLine());
        nextBlank = new int[G+1]; //빈 공간 가리키기
        
        for (int i = 1; i <= G; i++) {
            nextBlank[i] = i;
        }

        for (int i = 1; i <= P; i++) {
            int gi = Integer.parseInt(br.readLine());
            int blank = find(gi); //빈 공간 찾기
            if(blank == 0){
                break;
            }else{
                count++;
                nextBlank[blank] = nextBlank[blank-1];
            }
        }
        
        bw.write(String.valueOf(count));
        bw.close();
    }
    static int find(int gi){
        if(nextBlank[gi] == gi){
            return gi;
        }else{
            return nextBlank[gi] = find(nextBlank[gi]);
        }
    }
}
```
