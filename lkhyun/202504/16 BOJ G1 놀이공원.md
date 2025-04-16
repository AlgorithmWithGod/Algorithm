```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int M;
    static int[] ride;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        ride = new int[M + 1];

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= M; i++) {
            ride[i] = Integer.parseInt(st.nextToken());
        }

        long minTime = search(0, (long) N * 30); // 놀이기구에 있는 아이까지 포함해서 N이상인 시간임.
        minTime--;// 여기서 1을 빼면 새로운 애들이 아직 못탄 상태임.

        // N이 7일때 minTime-1 에서는 5명이 탔다고 가정하면 이때 빈곳에 다음 시간에 애들이 타서 7명이상이 된거지.
        long cnt = 0;
        for (int i = 1; i <= M; i++) { // 여기서 minTime-1에서 탔거나 타고 있는 애들 수를 셈
            cnt += minTime / ride[i];
            if (minTime % ride[i] != 0)
                cnt++;
        }
        cnt = N - cnt;// 그걸 전체에서 뺌. 그럼 다음 턴에 최소한 타야할 애들 수가 나옴.

        for (int i = 1; i <= M; i++) {
            if (minTime % ride[i] == 0) {// 앞에서부터 세서 나머지가 0이면 다음 시간에 바로 애들을 태울 수 있으니
                if (--cnt == 0) {// 타야할 애들이 다 타는 그 시점
                    bw.write(i + "");
                    break;
                }
            }
        }

        bw.close();
    }

    public static long search(long start, long end) {
        long l = start;
        long r = end;
        while (l < r) {
            long mid = (l + r) / 2; // 제한 시간
            long temp = 0;

            for (int i = 1; i <= M; i++) { // 놀이기구마다 mid 시간동안 태울 수 있는 아이의 수를 구함
                temp += mid / ride[i];
                if (mid % ride[i] != 0) // 놀이기구에서 아직 내리지 않은 아이도 셈
                    temp++;
            }

            if (temp < N) {// N명 다 처리 못함.
                l = mid + 1;
            } else {
                r = mid;
            }
        }
        return l;
    }
}



```
