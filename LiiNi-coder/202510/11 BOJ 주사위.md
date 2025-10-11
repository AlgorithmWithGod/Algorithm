```java
import java.io.*;
import java.util.*;

public class Main {
        private static int N;
    private static int[][] exposures3 = {
        {0, 1, 2},
        {0, 1, 3},
        {0, 3, 4},
        {0, 4, 2},
        {1, 2, 5},
        {1, 3, 5},
        {1, 0, 3},
        {1, 0, 2},
        {2, 1, 5},
        {2, 0, 1},
        {2, 0, 4},
        {2, 4, 5},
        {3, 0, 1},
        {3, 5, 1},
        {3, 4, 5},
        {3, 4, 0},
        {4, 2, 0},
        {4, 3, 0},
        {4, 3, 5},
        {4, 5, 2}
    };
    private static int[][] exposures2 = {
        {0, 1},
        {0, 2},
        {0, 3},
        {0, 4},
        {1, 0},
        {1, 2},
        {1, 5},
        {1, 3},
        {2, 0},
        {2, 1},
        {2, 5},
        {2, 4},
        {3, 0},
        {3, 1},
        {3, 5},
        {3, 4},
        {4, 0},
        {4, 2},
        {4, 3},
        {4, 5},
        {5, 1},
        {5, 2},
        {5, 3},
        {5, 4}
    };
    private static int[] Eyes;

    public static void main(String[] args)throws IOException {
        BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        Eyes = new int[6];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for(int i = 0; i < 6; i++) {
            Eyes[i] = Integer.parseInt(st.nextToken());
        }

        if(N == 1){
            System.out.println(Arrays.stream(Eyes).sum() - Arrays.stream(Eyes).max().getAsInt());
            return;
        }

        int min3 = Integer.MAX_VALUE;
        int min2 = Integer.MAX_VALUE;
        int min1 = Arrays.stream(Eyes).min().getAsInt();

        for(int[] exposure2 : exposures2) {
            int temp = 0;
            for(int i : exposure2) temp += Eyes[i];
            min2 = Math.min(temp, min2);
        }

        for(int[] exposure3 : exposures3) {
            int temp = 0;
            for(int i : exposure3) temp += Eyes[i];
            min3 = Math.min(temp, min3);
        }

        long nExposure3 = 4;
        long nExposure2 = (N - 2) * 8 + 4;
        long nExposure1 = (long)(N - 2) * (N - 2) + (long)(N - 2) * 4 * (N - 1);

        long answer = min3 * nExposure3 + min2 * nExposure2 + min1 * nExposure1;
        System.out.println(answer);
        br.close();
    }
}

```
