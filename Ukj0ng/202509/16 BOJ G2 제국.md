```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static TreeMap<String, Integer> country;
    private static Map<Integer, String> map;
    private static int[] uf;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        init();

        TreeSet<String> answer = new TreeSet<>();

        for (int i = 1; i <= N; i++) {
            answer.add(map.get(uf[i]));
        }

        bw.write(answer.size() + "\n");

        for (String element : answer) {
            bw.write("Kingdom of " + element + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        country = new TreeMap<>();
        map = new HashMap<>();
        uf = new int[N+1];

        for (int i = 1; i <= N; i++) {
            uf[i] = i;
        }

        for (int i = 1; i <= N; i++) {
            String[] input = br.readLine().split(" ");
            country.put(input[2], i);
            map.put(i, input[2]);
        }

        for (int i = 0; i < M; i++) {
            String[] input = br.readLine().split(" ");
            String country1 = input[2].split(",")[0];
            String country2 = input[4].split(",")[0];

            int index1 = country.get(country1);
            int index2 = country.get(country2);
            int result = Integer.parseInt(input[4].split(",")[1]);

            union(index1, index2, result);
        }

    }

    private static void union(int x, int y, int result) {
        int X = find(x);
        int Y = find(y);

        int[] temp;
        if (X == Y) {
            if (result == 1) temp = new int[]{0, x, Y};
            else temp = new int[]{0, X, y};

            for (int i = 1; i <= N; i++) {
                if (uf[i] == X) uf[i] = temp[result];
            }
        } else {
            if (result == 1) {
                for (int i = 1; i <= N; i++) {
                    if (uf[i] == Y) uf[i] = X;
                }
            } else {
                for (int i = 1; i <= N; i++) {
                    if (uf[i] == X) uf[i] = Y;
                }
            }
        }
    }

    private static int find(int x) {
        if(uf[x] == x) return x;

        return uf[x] = find(uf[x]);
    }
}
```
