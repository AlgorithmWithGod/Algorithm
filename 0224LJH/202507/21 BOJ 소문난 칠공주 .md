```java
import java.awt.*;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.HashSet;
import java.util.Set;


public class Main {
    static String[][] arr = new String[5][5];
    static Set<Point> set = new HashSet<>();
    static HashSet<Point> temp = new HashSet<>();
    static int[] dy = { -1,0,1,0};
    static int[] dx = { 0,1,0,-1};
    static int ans = 0;


    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        for (int i = 0; i < 5; i++) {
            arr[i] = br.readLine().split("");
        }
    }

    private static void process() throws IOException {
        combination(0,0);
    }

    private static void combination(int num, int idx) {
        if ( idx == 7) {
            check();
            return;
        }

        for (int i = num; i < 25; i++){
            int y = i/5;
            int x = i%5;

            set.add(new Point(x, y));
            combination(i+1, idx+1);
            set.remove(new Point(x, y));
        }
    }

    private static void check() {


        Point first = set.iterator().next();

        int sCount = 0;
        for (Point p : set) {
            if(arr[p.y][p.x].equals("S") ) sCount++;
        }


        if (sCount >= 4 && checkConnected(first)) {
            ans++;
        }

    }

    private static boolean checkConnected(Point first) {
        temp = new HashSet<>();
        temp.add(first);

        for (int i = 0 ; i < 7; i++){
            for (Point p : set) {
                if (temp.contains(p)) continue;

                boolean isConnected = false;
                for (int j = 0; j <4 ; j++){
                    int ny = p.y + dy[j];
                    int nx = p.x + dx[j];

                    if (temp.contains(new Point(nx, ny))) {
                        isConnected = true;
                        break;
                    }
                }

                if (isConnected) {
                    temp.add(p);
                }
            }
        }

        return temp.size() == 7;

    }


    private static void print()  {
        System.out.println(ans);
    }



}

```