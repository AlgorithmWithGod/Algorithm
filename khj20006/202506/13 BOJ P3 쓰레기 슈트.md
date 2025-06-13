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
    double x, y;
    Point(double x, double y) {
        this.x = x;
        this.y = y;
    }
}

public class Main {

    static IOController io;

    //

    static int N;
    static Point[] A;
    static List<Point> H;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        N = io.nextInt();
        for(int t=1;N != 0;t++) {
            init();
            solve(t);
            N = io.nextInt();
        }

        io.close();

    }

    public static void init() throws Exception {

        A = new Point[N];
        for(int i=0;i<N;i++) A[i] = new Point(io.nextInt(), io.nextInt());
        H = new ArrayList<>();

    }

    static void solve(int tc) throws Exception {

        construct();
        double ans = 1e9;
        for(int i=0;i<H.size();i++) {
            Point a = H.get(i), b = H.get((i+1)%H.size());
            double res = 0;
            for(int j=0;j<H.size();j++) if(j != i && j != (i+1)%H.size()){
                Point c = H.get(j);
                res = Math.max(res, get(a, b, c));
            }
            ans = Math.min(ans, res);
        }

        int answer = (int)Math.ceil(ans * 100 - 1e-15);

        String p1 = Integer.toString(answer/100);
        String p2 = Integer.toString(answer%100);
        if(p2.length() == 1) p2 = "0" + p2;

        io.write("Case " + tc + ": " + p1 + "." + p2 + "\n");

    }

    static void construct() throws Exception {

        Arrays.sort(A, (a,b) -> {
            if(a.x == b.x) return Double.compare(a.y,b.y);
            return Double.compare(a.x,b.x);
        });

        List<Point> lower = new ArrayList<>();
        List<Point> upper = new ArrayList<>();
        for(int i=0;i<N;i++) {
            Point p = A[i];
            while(lower.size()>1 && ccw(lower.get(lower.size()-2), lower.get(lower.size()-1), p) <= 0) lower.remove(lower.size()-1);
            lower.add(p);
        }
        for(int i=0;i<N;i++) {
            Point p = A[i];
            while(upper.size()>1 && ccw(upper.get(upper.size()-2), upper.get(upper.size()-1), p) >= 0) upper.remove(upper.size()-1);
            upper.add(p);
        }

        for(int i=0;i<lower.size()-1;i++) H.add(lower.get(i));
        for(int i=upper.size()-1;i>0;i--) H.add(upper.get(i));

    }

    static int ccw(Point a, Point b, Point c) {
        double res = a.x*b.y + b.x*c.y + c.x*a.y - (b.x*a.y + c.x*b.y + a.x*c.y);
        if(res > 0) return 1;
        if(res < 0) return -1;
        return 0;
    }

    static double get(Point a, Point b, Point c) {

        double dx = b.x-a.x, dy = b.y-a.y;

        // y = dy/dx (x - a.x) + a.y
        // dx*y = dy*x - dy*a.x + dx*a.y
        // dy*x - dx*y - dy*a.x + dx*a.y = 0

        double ans = Math.abs(dy*c.x - dx*c.y + a.y*dx - a.x*dy) / Math.sqrt(dy*dy + dx*dx);
        return ans;

    }

}
```
