```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;


public class Main {

    static int target,idx;
    static long[] decreasingNum;


    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        target = Integer.parseInt(br.readLine());
        decreasingNum = new long[1000001];
        Arrays.fill(decreasingNum, -1);
        idx = 0;
    }

    private static void process() throws IOException {
        for (int i = 1; i <= 10; i++){
            findNum(i-1,0,10);
        }

    }

    private static void findNum(int curPos, long curNum,int limit) {
        if (curPos == -1){
            decreasingNum[idx++] = curNum;
        }

        for (int i = 0; i < limit; i++){
            long tempNum = (long) (curNum + Math.pow(10,curPos) * i);
            findNum(curPos-1,tempNum,i);

        }
    }


    private static void print() {
        System.out.println(decreasingNum[target]);
    }
}
```