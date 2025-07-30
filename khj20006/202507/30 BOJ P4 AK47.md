```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    public static void main(String[] args) throws Exception {

        int T = Integer.parseInt(br.readLine());
        while (T-- > 0) {

            int N = Integer.parseInt(br.readLine());

            if(N <= 47) naive(N);
            else window(N);

        }

    }

    static void naive(int N) throws Exception {
        int a = -1, b = -1;
        for(int i=1;i<=N;i++) {
            if(shout(i,i)) {
                if(a == -1) a = i;
                else b = i;
            }
        }
        bw.write("! " + a + " " + b + "\n");
        bw.flush();
    }

    static void window(int N) throws Exception {
        int s = 2, e = (N+2)/2 + 1;
        int start = s-1, end = e-1;

        // 맨 처음이 O인 경우
        if(shout(s-1,e-1)) {
            bw.write("! " + find(1,e-1) + " " + find(e,N) + "\n");
            bw.flush();
            return;
        }

        while(e <= N) {
            if(shout(s,e)) {
                if(s == 45 && e == 91) {
                    if(shout(46,92)) {
                        if(shout(46,46)) {
                            bw.write("! 44 46\n");
                            bw.flush();
                        }
                        else {
                            bw.write("! 44 47\n");
                            bw.flush();
                        }
                    }
                    else {
                        if(shout(91,91)) {
                            bw.write("! 91 92\n");
                            bw.flush();
                        }
                        else {
                            bw.write("! 44 45\n");
                            bw.flush();
                        }
                    }
                }
                else if(e < N && shout(e,e)) {
                    bw.write("! " + e + " " + find(e+1,N) + "\n");
                    bw.flush();
                }
                else {
                    bw.write("! " + (s-1) + " " + find(s,end) + "\n");
                    bw.flush();
                }
                return;
            }
            s++;
            e++;
        }
        bw.write("! " + end + " " + (end-1) + "\n");
        bw.flush();
    }

    static int find(int s, int e) throws Exception {
        int m = (s+e)>>1;
        while(s<e) {
            if(shout(s,m)) e = m;
            else {
                s = m+1;
                if(s == e) return s;
            }
            m = (s+e)>>1;
        }
        return m;
    }

    static boolean shout(int l, int r) throws Exception {
        bw.write("AK " + l + " " + r + "\n");
        bw.flush();
        return br.readLine().charAt(0) == 'O';
    }

}
```
