```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
static int cityCnt, ans;
static int[][] distance;

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        cityCnt = Integer.parseInt(br.readLine());
        distance = new int[cityCnt][cityCnt];
        ans = 0;

        for (int i = 0; i < cityCnt; i++){
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < cityCnt; j++){
                distance[i][j] = Integer.parseInt(st.nextToken());
            }
        }
    }

    private static void process() {
        for (int i = 0; i < cityCnt; i++){
            for (int j = i; j < cityCnt; j++){
                if ( i == j) continue;
                if (distance[i][j] != distance[j][i]){
                    // i->j와 j->i는 같아야함
                    ans = -1;
                    return;
                }

                boolean isDirectlyConnected = true;

                for (int k = 0; k < cityCnt; k++){
                    if ( i == k || j ==k) continue;
                    int tempDis = distance[i][k] + distance[k][j];
                    
                    if (tempDis < distance[i][j]){
                        //지금 명시된 길이가 두개의 길을 이은것 보다 짧음 -> 불가능
                        ans =-1;
                        return;
                    } else if ( tempDis== distance[i][j]) {
                        isDirectlyConnected = false;
                        break;
                    }
                }

                if (isDirectlyConnected) {
                    ans += distance[i][j];
                }
            }
        }
    }



    private static void print() {
        System.out.print(ans);
    }
}
```
