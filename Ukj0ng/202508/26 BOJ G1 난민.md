```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static PriorityQueue<int[]> upperQueue;
    private static PriorityQueue<int[]> lowerQueue;
    private static int N, median;
    private static long sum;
    public static void main(String[] args) throws IOException {
        init();

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        long upperVal = 0;
        long lowerVal = 0;
        median = 0;
        sum = 0;
        long xSum = 0;

        upperQueue = new PriorityQueue<>((o1, o2) -> Integer.compare(o1[1], o2[1]));
        lowerQueue = new PriorityQueue<>((o1, o2) -> Integer.compare(o2[1], o1[1]));

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());

            lowerQueue.add(new int[]{x, y});
            lowerVal += y;
            xSum += Math.abs(x);

            if (upperQueue.size() + 1 == lowerQueue.size()) {
                if (!upperQueue.isEmpty() && upperQueue.peek()[1] < lowerQueue.peek()[1]) {
                    upperVal += (lowerQueue.peek()[1] - upperQueue.peek()[1]);
                    lowerVal += (upperQueue.peek()[1] - lowerQueue.peek()[1]);
                    swap();
                }
            } else if (upperQueue.size() + 2 == lowerQueue.size()) {
                upperVal += lowerQueue.peek()[1];
                lowerVal -=  lowerQueue.peek()[1];
                upperQueue.add(lowerQueue.poll());
            }

            median = lowerQueue.peek()[1];
            long ySum = ((long)median * lowerQueue.size() - lowerVal + upperVal - (long)median * upperQueue.size());
            long totalSum = xSum + ySum;
            bw.write(median + " " + totalSum + "\n");
        }
    }

    private static void swap() {
        int[] temp = lowerQueue.poll();
        lowerQueue.add(upperQueue.poll());
        upperQueue.add(temp);
    }
}

```
