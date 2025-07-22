```java
import java.awt.Point;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {

    //거울 만날 시 진행 방향
    //오른쪽 <-> 위
    // 아래 <-> 왼쪽

    static final int MIRROR = -1;

    static int height,width,direction;
    static int [][] arr;
    static int[] dy = {1,0,-1,0}; // 아래 오른쪽 위쪽 왼쪽 순
    static int[] dx = {0,1,0,-1};
    static int[] ans;

    static HashMap<Integer, Point> map = new HashMap<>();

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        height = Integer.parseInt(st.nextToken());
        width = Integer.parseInt(st.nextToken());
        arr = new int[height+2][width+2];
        ans = new int[height*2 + width*2+1];

        for (int i = 1; i <= height; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= width; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken()) * (-1);
            }
        }

    }

    private static void process() throws IOException {
        markHoleNumber();
        for (int i = 1; i < ans.length; i++) {
            if (ans[i] != 0) continue;
            Point p = map.get(i);

            if (p.x == 0) direction = 1; //오른쪽으로
            else if (p.y == height+1)  direction = 2; //위로
            else if (p.x == width+1) direction = 3; //왼쪽으로
            else direction = 0; // 아래로

            processLightMove(i);
        }



    }

    private static void processLightMove(int pointNum) {
        Point p = map.get(pointNum);
        int y = p.y;
        int x = p.x;

        while (true) {
            y += dy[direction];
            x += dx[direction];

            if (arr[y][x] > 0) {
                ans[pointNum] = arr[y][x];
                ans[ans[pointNum]] = pointNum;
                break;
            }

            if (arr[y][x] == MIRROR){
                switch (direction) {
                    case 0: direction = 3; break;
                    case 1: direction = 2; break;
                    case 2: direction = 1; break;
                    case 3: direction = 0; break;
                }
            }


        }
    }

    private static void markHoleNumber() {
        // 구멍 번호 마킹
        direction = 0;
        int num = 1;
        int y = 1;
        int x = 0;
        while ( y != 0 || x != 0){
            if ( (y == height +1 || y == 0) && (x == 0 || x == width + 1) ) {
                direction++;
            } else{
                map.put(num,new Point(x,y));
                arr[y][x] = num++;
            }

            y += dy[direction];
            x += dx[direction];
        }

    }


    private static void print() {
        for (int i = 1; i < ans.length; i++) {
            System.out.print(ans[i] + " ");
        }
    }
}

```