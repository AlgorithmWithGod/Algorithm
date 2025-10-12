```
import java.io.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] uf, size;
    private static int N;
    private static long d, bridge;

    public static void main(String[] args) throws IOException {
        init();

        bw.flush();
        bw.close();
        br.close();
    }
    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        d = 0;
        bridge = 0;

        uf = new int[N+1];
        size = new int[N+1];

        for (int i = 1; i <= N; i++) {
            uf[i] = i;
            size[i] = 1;
        }

        for (int i = 0; i < N-1; i++) {
            int a = Integer.parseInt(br.readLine());
            int b = a+1;

            int A = find(a);
            int B = find(b);

            long sizeA = size[A];
            long sizeB = size[B];

            d -= ((sizeA*(sizeA-1)/2) + (sizeB*(sizeB-1)/2));
            bridge -= ((sizeA*(sizeA*sizeA-1))/6 + (sizeB*(sizeB*sizeB-1))/6);
            union(A, B);

            long newSize = sizeA + sizeB;

            d += newSize*(newSize-1)/2;
            bridge += newSize*(newSize*newSize-1)/6;

            bw.write(d + " " + bridge + "\n");
        }
    }

    private static void union(int X, int Y) {
        if (X == Y) return;

        if (size[X] < size[Y]) {
            uf[X] = Y;
            size[Y] += size[X];
        } else {
            uf[Y] = X;
            size[X] += size[Y];
        }
    }

    private static int find(int x) {
        if (uf[x] == x) return x;

        return uf[x] = find(uf[x]);
    }
}
```
