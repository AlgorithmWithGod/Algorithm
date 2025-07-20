```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;


public class Main {

    static int len,changeCnt,left;
    static int[] arr;


    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        len = Integer.parseInt(br.readLine());
        arr = new int[len];

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < len; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        changeCnt = Integer.parseInt(br.readLine());
        left = changeCnt;
    }

    private static void process() {
        //i번 인덱스를 조사하는데 n번의 기회가 남았을 때,
        //지금 인덱스에서 1~n칸만큼 떨어진 숫자들 중 가장 큰 값 찾음.
        //제일 큰 값을 i번 인덱스에 넣고, 나머지 값들은 다 한칸씩 미룸
        //남은 횟수 갱신
        //이를 끝까지 가거나, 기회를 다 쓰면 끝
        int curIdx = 0;
        while (curIdx < len-1 && left > 0 ){
            int max = arr[curIdx];
            int maxIdx = curIdx;

            for (int i = curIdx+1; (i < len && i <= curIdx + left  ); i++) {
                if (arr[i] > max){
                    max = arr[i];
                    maxIdx = i;
                }
            }

            rangeSwap(curIdx, maxIdx);
            left -= maxIdx - curIdx;
            curIdx++;
        }


    }

    private static void rangeSwap(int fromIdx, int toIdx) {
        for (int i = toIdx; i > fromIdx; i--) {
            swap(i, i-1);
        }
    }

    private static void swap(int tIdx1, int tIdx2) {
        int tmp = arr[tIdx1];
        arr[tIdx1] = arr[tIdx2];
        arr[tIdx2] = tmp;
    }



    private static void print()  {
        for (int i = 0; i < len; i++) {
            System.out.print(arr[i] + " ");
        }
    }



}



```