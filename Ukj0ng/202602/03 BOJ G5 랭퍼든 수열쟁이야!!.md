```
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] arr;
    private static boolean[] visited;
    private static int N, X, Y, answer;

    public static void main(String[] args) throws IOException {
        init();
        arr[X] = Y-X-1;
        arr[Y] = Y-X-1;
        visited[Y-X-1] = true;
        make(1);

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        X = Integer.parseInt(st.nextToken());
        Y = Integer.parseInt(st.nextToken());

        arr = new int[2*N+1];
        visited = new boolean[N+1];
    }

    private static void make(int index) {
        if (index == 2*N+1) {
            answer++;
            return;
        }

        if (arr[index] != 0) make(index+1);
        else {
            for (int i = 1; i <= N; i++) {
                if (!visited[i]) {
                    if (index+i+1 <= 2*N && arr[index+i+1] == 0) {
                        arr[index] = i;
                        arr[index+i+1] = i;
                        visited[i] = true;
                        make(index+1);
                        visited[i] = false;
                        arr[index] = 0;
                        arr[index+i+1] = 0;
                    }
                }
            }
        }
    }
}
```
