```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;


public class Main {


    static StringBuilder sb = new StringBuilder();
    static int cityCnt,planCityCnt;
    static int[][] arr;
    static int[] plan,parent;


    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        cityCnt = Integer.parseInt(br.readLine());
        planCityCnt = Integer.parseInt(br.readLine());
        arr = new int[cityCnt][cityCnt];
        parent = new int[cityCnt];
        for (int i = 0; i < cityCnt; i++) {
            parent[i] = i;
        }
        plan = new int[planCityCnt];

        for (int i = 0; i < cityCnt; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < cityCnt; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < planCityCnt; i++) {
            plan[i] = Integer.parseInt(st.nextToken())-1;
        }

    }

    private static void process() throws IOException {
        for (int i = 0; i < cityCnt; i++) {
            for (int j = 0; j < cityCnt; j++) {
                if (arr[i][j] == 1) union(i,j);
            }
        }

        for (int i = 1; i < planCityCnt; i++) {
            int preRoot = find(plan[i-1]);
            int curRoot = find(plan[i]);
            if (preRoot != curRoot) {
                System.out.println("NO");
                return;
            }
        }

        System.out.println("YES");

    }

    private static void union(int a, int b) {
        int aRoot = find(a);
        int bRoot = find(b);

        if (aRoot == bRoot) return;

        if (aRoot > bRoot) {
            parent[bRoot] = aRoot;
        } else {
            parent[aRoot] = bRoot;
        }

    }

    private static int find(int x) {
        if (x == parent[x]) return x;

        return parent[x] = find(parent[x]);
    }



    private static void print() {
        System.out.print(sb.toString());
    }
}
```