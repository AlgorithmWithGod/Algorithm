```java
import java.awt.Point;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;
import java.util.StringTokenizer;


public class Main {

    static final int APPLE = -1;
    static final int EMPTY = 0;
    static final int SNAKE = 1;

    static Change[] change;
    static Queue<Point> snake;

    static int[][] arr;
    static int[] dy = {0,1,0,-1}; // 오른쪽->아래->왼쪽->위
    static int[] dx = {1,0,-1,0};
    static int size,appleCnt,changeCnt,direction,cur;

    static class Change{
        int time;
        int direction;
        public Change(int time, int direction){
            this.time = time;
            this.direction = direction;
        }
    }


    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        snake = new LinkedList<>();
        size = Integer.parseInt(br.readLine());
        appleCnt = Integer.parseInt(br.readLine());
        direction = 0;
        snake.add(new Point(0,0));

        arr = new int[size][size];

        for (int i = 0; i < appleCnt; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int y = Integer.parseInt(st.nextToken())-1;
            int x = Integer.parseInt(st.nextToken())-1;
            arr[y][x] = APPLE;
        }

        changeCnt = Integer.parseInt(br.readLine());
        change = new Change[changeCnt];
        for (int i = 0; i < changeCnt; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int time = Integer.parseInt(st.nextToken());
            int direction = (st.nextToken().equals("L"))?-1:1;
            change[i] = new Change(time, direction);
        }
    }

    private static void process() throws IOException {
        Point head = snake.peek();
        cur = 0;
        int changeIdx= 0;

        while (true) {
            cur++;
            int ny =  head.y + dy[direction];
            int nx = head.x +  dx[direction];

            if (ny < 0 || nx < 0 || ny >= size || nx >= size) break;
            if (arr[ny][nx] == SNAKE) break;

            Point nHead = new Point(nx, ny);

            snake.add(nHead);
            if (arr[ny][nx] == EMPTY) {
                Point tail = snake.poll();
                arr[tail.y][tail.x] = EMPTY;
            }
            //사과를 만난경우 그냥 진행하면됨

            arr[ny][nx] = SNAKE;

            head = nHead;

            if (changeIdx < changeCnt) {
                Change c =  change[changeIdx];
                if (cur < c.time) continue;

                direction = (direction +  c.direction + 4)%4 ;
                changeIdx++;
            }

        }

    }

    private static void print() {
        System.out.println(cur);
    }
}
```
