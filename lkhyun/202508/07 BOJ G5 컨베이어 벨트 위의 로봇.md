```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());
        
        int[] belt = new int[2 * N];
        boolean[] robot = new boolean[2 * N];
        
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < 2 * N; i++) {
            belt[i] = Integer.parseInt(st.nextToken());
        }
        
        int step = 0;
        
        while (true) {
            step++;
            
            int tempBelt = belt[2 * N - 1];
            boolean tempRobot = robot[2 * N - 1];
            
            for (int i = 2 * N - 1; i > 0; i--) {
                belt[i] = belt[i - 1];
                robot[i] = robot[i - 1];
            }
            
            belt[0] = tempBelt;
            robot[0] = tempRobot;

            if (robot[N - 1]) {
                robot[N - 1] = false;
            }
            
            for (int i = N - 2; i >= 0; i--) {
                if (robot[i] && !robot[i + 1] && belt[i + 1] > 0) {
                    robot[i] = false;
                    robot[i + 1] = true;
                    belt[i + 1]--;
                    
                    if (i + 1 == N - 1) {
                        robot[i + 1] = false;
                    }
                }
            }
            
            if (!robot[0] && belt[0] > 0) {
                robot[0] = true;
                belt[0]--;
            }
            
            int zeroCount = 0;
            for (int i = 0; i < 2 * N; i++) {
                if (belt[i] == 0) {
                    zeroCount++;
                }
            }
            
            if (zeroCount >= K) {
                break;
            }
        }
        
        bw.write(step+"");
        bw.close();
    }
}
```
