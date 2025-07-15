```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static int kidCnt, toyCnt,  ans;
    static long start, end,minTime;
    static int[] toyTime;

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        kidCnt = Integer.parseInt(st.nextToken());
        toyCnt = Integer.parseInt(st.nextToken());
        toyTime = new int[toyCnt];

        start = 0;
        end = 2000_000_000_00l;

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < toyCnt; i++) {
            toyTime[i] = Integer.parseInt(st.nextToken());
        }
    }

    private static void process() {
        if (kidCnt <= toyCnt) {
            ans = kidCnt;
            return;
        }

        //마지막 사람이 탑승하는 시간 구함
        calculateProperTime();

        int curKidCnt = 0;
        List<Integer> minRemainIdx = new ArrayList<>();
        int minRemain = 30;

        for (int i = 0; i < toyCnt; i++) {
            curKidCnt += minTime / toyTime[i] + 1;

            if (minRemain > minTime % toyTime[i]) {
                minRemain = (int) (minTime % toyTime[i]);
                minRemainIdx = new ArrayList<>();
                minRemainIdx.add(i);
            } else if (minRemain == minTime % toyTime[i]) {
                minRemainIdx.add(i);
            }
        }

        if (curKidCnt == kidCnt){
            ans = minRemainIdx.get(minRemainIdx.size()-1)+1;
        } else{
            int diff = (curKidCnt - kidCnt)%minRemainIdx.size();
            ans = minRemainIdx.get(minRemainIdx.size()-1-diff) + 1;
        }

    }

    private static void calculateProperTime() {
        long mid =  ((start + end) / 2);
        minTime = Long.MAX_VALUE;


        while (start < end) {

            //이번 탐색에서 놀이기구를 이용한 총 인원
            long peopleCnt = 0;

            for (int i = 0; i < toyCnt; i++) {
                //총시간을 각 놀이기구 이용시간으로 나눈 몫 + 1;
                peopleCnt += mid/toyTime[i] + 1;
            }

            // 크거나 같음 -> 암튼 이 시간내에 꼬마들이 다 이용함.
            if(peopleCnt >= kidCnt) {
                if (mid < minTime) {
                    minTime = mid;
                    end = mid;
                }

                if (peopleCnt == kidCnt){
                    minTime = mid;
                    break;
                }
            } else  {
                // 목표보다 아이들이 이용 못함 -> 더 큰쪽 조사
                start = mid+1;
            }

            mid = ((start + end) / 2);
        }


    }


    private static void print()  {
        System.out.println(ans);
    }



}

```