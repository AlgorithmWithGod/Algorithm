```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
    static long ans,max,min;
    static int len;
    static boolean[] powerNoNoNum;

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        min = Long.parseLong(st.nextToken());
        max = Long.parseLong(st.nextToken());
        len = (int) (max - min+1);

        powerNoNoNum = new boolean[len];
        Arrays.fill(powerNoNoNum,true);
        ans = 0;

    }

    private static void process() {
        for (long i = 2; i * i <= max; i++){
            long powerNum = i * i;
            if (powerNum > max) break;

            long curIdx;
            if (powerNum < min) {
                long temp = (min + powerNum - 1) / powerNum;
                curIdx = temp * powerNum - min;
            } else {
                curIdx = powerNum - min;
            }

            while(curIdx < len){
                powerNoNoNum[(int) curIdx] = false;
                curIdx += powerNum;
            }
        }

        for (int i = 0; i < powerNoNoNum.length; i++){
            if (powerNoNoNum[i]) ans++;
        }
    }




    private static void print()  {
        System.out.println(ans);
    }



}

```