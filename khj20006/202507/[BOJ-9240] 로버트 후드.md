```java
import java.util.*;
import java.io.*;

class IOController {
    BufferedReader br;
    BufferedWriter bw;
    StringTokenizer st;

    public IOController() {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer("");
    }

    String nextLine() throws Exception {
        String line = br.readLine();
        st = new StringTokenizer(line);
        return line;
    }

    String nextToken() throws Exception {
        while (!st.hasMoreTokens()) nextLine();
        return st.nextToken();
    }

    int nextInt() throws Exception {
        return Integer.parseInt(nextToken());
    }

    long nextLong() throws Exception {
        return Long.parseLong(nextToken());
    }

    double nextDouble() throws Exception {
        return Double.parseDouble(nextToken());
    }

    void close() throws Exception {
        bw.flush();
        bw.close();
    }

    void write(String content) throws Exception {
        bw.write(content);
    }

}

class Point {
    int x, y;
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    int ccw(Point p1, Point p2) {
        int res = p1.x*p2.y + p2.x*this.y + this.x*p1.y - (p2.x*p1.y + this.x*p2.y + p1.x*this.y);
        if(res < 0) return -1;
        if(res > 0) return 1;
        return 0;
    }

    double dist(Point o) {
        return Math.sqrt((this.x - o.x) * (this.x - o.x) + (this.y - o.y) * (this.y - o.y));
    }
}

public class Main {

    static IOController io;

    //

    static int N;
    static Point[] a;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();
    }

    public static void init() throws Exception {

        N = io.nextInt();
        a = new Point[N];
        for(int i=0;i<N;i++) a[i] = new Point(io.nextInt(),io.nextInt());

    }

    static void solve() throws Exception {

        // 볼록 껍질 만들기
        Arrays.sort(a, (a,b) -> a.x==b.x ? a.y-b.y : a.x-b.x);
        List<Point> lower = new ArrayList<>();
        List<Point> upper = new ArrayList<>();
        for(Point p:a) {
            while(lower.size() > 1 && p.ccw(lower.get(lower.size()-2), lower.get(lower.size()-1)) <= 0) lower.remove(lower.size()-1);
            lower.add(p);
            while(upper.size() > 1 && p.ccw(upper.get(upper.size()-2), upper.get(upper.size()-1)) >= 0) upper.remove(upper.size()-1);
            upper.add(p);
        }

        List<Point> hull = new ArrayList<>();
        for(int i=0;i<lower.size()-1;i++) hull.add(lower.get(i));
        for(int i=upper.size()-1;i>0;i--) hull.add(upper.get(i));



        // 회전하는 캘리퍼스 구현
        double ans = 0;
        N = hull.size();

        int j = 1;
        for(int i=0;i<N;i++) {
            Point p1 = hull.get(i);
            Point p2 = hull.get((i+1)%N);
            Point p3 = hull.get(j);
            Point p4 = hull.get((j+1)%N);
            Point p5 = new Point(p4.x - (p3.x - p2.x), p4.y - (p3.y - p2.y));
            while(p5.ccw(p1, p2) > 0) {
                j = (j+1)%N;
                p3 = hull.get(j);
                p4 = hull.get((j+1)%N);
                p5 = new Point(p4.x - (p3.x - p2.x), p4.y - (p3.y - p2.y));
            }
            ans = Math.max(ans, p1.dist(p3));
        }
        io.write(ans + "\n");

    }

}
```
