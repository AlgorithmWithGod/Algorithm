```java
import java.awt.Point;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;


public class Main {

    static final int DAY = 1440;
    static final int NIGHT = 1320;
    static final int MORNING = 480;
    static final int HOUR = 60;

    static String[] rawTime;
    static int[] playTimes;
    static int tc, curBill,curTime,playTime;

    static StringBuilder sb = new StringBuilder();


    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        tc = Integer.parseInt(br.readLine());
        rawTime = new String[tc];
        playTimes = new int[tc];
        for (int i = 0; i < tc; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            rawTime[i] = st.nextToken();
            playTimes[i] = Integer.parseInt(st.nextToken());
        }

    }

    private static void process() throws IOException {
        for (int i = 0; i < tc; i++) {
            System.out.println();
            String rawTarget =  rawTime[i];

            int hour = Integer.parseInt(rawTarget.substring(0,2));
            int minute = Integer.parseInt(rawTarget.substring(3,5));

            playTime = playTimes[i];
            curTime = hour * 60 + minute;
            curBill = 0;

            while (playTime > 0) {
                if (curTime  < MORNING || curTime >= NIGHT) {
                    toMorning();
                } else {
                    toNight();
                }
            }

            sb.append(curBill).append("\n");
        }
    }

    private static void toNight() {
        int leftTimeToNight = NIGHT -  curTime;
        if ( leftTimeToNight > playTime) { // 밤에 도달 못함
            curBill += (playTime/HOUR) * 1000;
            if (playTime%HOUR != 0) curBill += 1000;
            playTime = 0;
        } else {
            if (playTime - leftTimeToNight < 300) {
                curBill += (playTime/HOUR) * 1000;
                if (playTime%HOUR != 0) curBill += 1000;
                playTime = 0;
            } else {
                curBill += (leftTimeToNight/HOUR) * 1000;
                if (leftTimeToNight%HOUR != 0) curBill += 1000;
                playTime -= leftTimeToNight;
                curTime = NIGHT;
            }
        }
    }

    private static void toMorning() {
        int leftTimeToMorning = MORNING - curTime;
        if ( leftTimeToMorning < 0) leftTimeToMorning += DAY;

        if ( leftTimeToMorning >= 300 ) {
            if (playTime >= 300){
                curBill += 5000;
                playTime -= leftTimeToMorning;
                curTime = MORNING;
            } else {
                curBill += (playTime/HOUR) * 1000;
                if (playTime%HOUR != 0) curBill += 1000;
                playTime = 0;
            }
        } else {
            if(leftTimeToMorning > playTime  ) {
                int tempBill = (leftTimeToMorning/HOUR) * 1000;
                if(leftTimeToMorning%HOUR != 0) tempBill += 1000;

                curBill += tempBill;
                curTime += (tempBill/1000)*60;
                playTime -= (tempBill/1000)*60;
            } else {
                curBill += (playTime/HOUR) * 1000;
                if (playTime%HOUR != 0) curBill += 1000;
                playTime = 0;
            }
        }

        if (curTime > DAY) curTime -= DAY;

    }

    private static void print() {
        System.out.print(sb.toString());
    }
}
```