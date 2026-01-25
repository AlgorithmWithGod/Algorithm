```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] arr;
    private static int N, G, B, D;
    private static long answer;

    public static void main(String[] args) throws IOException {
        init();
        if (B < arr[0][0]) bw.write(-1 + "\n");
        else {
            B -= arr[0][0];
            answer = greedy();
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        G = Integer.parseInt(st.nextToken());
        B = Integer.parseInt(st.nextToken());
        D = Integer.parseInt(st.nextToken());

        arr = new int[N][2];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int X = Integer.parseInt(st.nextToken());
            int Y = Integer.parseInt(st.nextToken());
            arr[i][0] = X;
            arr[i][1] = Y;
        }

        Arrays.sort(arr, (o1, o2) -> Integer.compare(o1[0], o2[0]));
    }

    private static long greedy() {
        long result = 0;
        int pos = arr[0][0];

        int current = 0;

        while (current < N-1) {
            int next = -1;

            for (int i = current+1; i < N; i++) {
                if (arr[i][0] > arr[current][0] + G) break;

                if (arr[i][1] < arr[current][1]) {
                    next = i;
                    break;
                }
            }

            if (next == -1) {
                long remain = G-B;
                result += arr[current][1]*remain;
                B = G;
                for (int i = current; i < N; i++) {
                    if (pos + G >= arr[i][0]) {
                        next = i;
                    }
                }
            } else {
                long remain = arr[next][0]-pos;
                result += arr[current][1]*remain;
                B += (int)remain;
            }

            int dist = arr[next][0] - pos;
            pos = arr[next][0];
            B -= dist;
            current = next;
        }

        if (pos + G >= D) {
            result += (long)(D-pos)*arr[current][1];
        } else {
            result = -1;
        }

        return result;
    }
}
```
