```java
import java.util.*;
import java.io.*;
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int H = 0;
    static int W = 0;
    static int[] world;
    static int answer = 0;
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        H = Integer.parseInt(st.nextToken());
        W = Integer.parseInt(st.nextToken());
        world = new int[W];

        st = new StringTokenizer(br.readLine());
        for(int i=0;i<W;i++){
            world[i] = Integer.parseInt(st.nextToken());
        }

        boolean flag = true;
        while(flag){
            flag = false;
            for(int k=1;k<W-1;k++){
                int left = 0;
                for(int i=1;i<=k;i++) { //왼쪽 탐색
                    if (world[k - i] > world[k]) {
                        left = i;
                        break;
                    }
                }
                int right = 0;
                for(int i=1;i<W-k;i++){ //오른쪽 탐색
                    if (world[k + i] > world[k]) {
                        right = i;
                        break;
                    }
                }
                if(left!=0 && right!=0){
                    if(world[k]<H){
                        world[k]++;
                        flag = true;
                        answer++;
                    }
                }
            }
        }
        bw.write(answer+"");
        bw.close();
    }
}

```
