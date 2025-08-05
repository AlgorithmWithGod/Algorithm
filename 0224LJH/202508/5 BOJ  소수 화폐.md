```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;


public class Main {

    static final int WAR = 2;
    static final int UNION = 1;

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringBuilder sb = new StringBuilder();
    static int[] countryPower,parent;
    static boolean[] isAlive;
    static int countryCnt, recordCnt,ans;
    static List<Integer> ansList = new ArrayList<>();

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
        
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        countryCnt = Integer.parseInt(st.nextToken());
        recordCnt = Integer.parseInt(st.nextToken());
        countryPower = new int[countryCnt];
        parent = new int[countryCnt];
        isAlive = new boolean[countryCnt];
        Arrays.fill(isAlive, true);

        for (int i = 0; i < countryCnt; i++) {
            countryPower[i] = Integer.parseInt(br.readLine());
            parent[i] = i;
        }
    }

    private static void process() throws IOException {
        for (int i = 0; i < recordCnt; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int order = Integer.parseInt(st.nextToken());
            int a = Integer.parseInt(st.nextToken())-1;
            int b = Integer.parseInt(st.nextToken())-1;

            if (order == UNION) {
                union(a, b);
            } else{
                war(a,b);
            }
        }

        for (int i = 0; i < countryCnt; i++) {
            if (!isAlive[i]) continue;
            int iRoot = find(i);
            if (iRoot != i) continue;
            if (isAlive[iRoot]) {
                ans++;
                ansList.add(countryPower[iRoot]);
            }
        }



    }

    private static void war(int a, int b) {
        int aRoot = find(a);
        int bRoot = find(b);

        if (aRoot == bRoot) return;

        int aPower = countryPower[aRoot];
        int bPower = countryPower[bRoot];
        if (aPower > bPower) {
            countryPower[aRoot] -= bPower;
            countryPower[bRoot] = 0;
            parent[bRoot] = aRoot;
            isAlive[bRoot] = false;
        } else if (aPower < bPower) {
            countryPower[bRoot] -= aPower;
            countryPower[aRoot] = 0;
            parent[aRoot] = bRoot;
            isAlive[aRoot] = false;
        } else{
            countryPower[aRoot]  = 0;
            countryPower[bRoot] = 0;
            isAlive[aRoot] = false;
            isAlive[bRoot] = false;
        }


    }

    private static void union(int a, int b) {
        int aRoot = find(a);
        int bRoot = find(b);

        if (aRoot == bRoot) return;

        int aPower = countryPower[aRoot];
        int bPower = countryPower[bRoot];

        if (aPower >= bPower) {
            countryPower[aRoot] += bPower;
            countryPower[bRoot] = 0;
            parent[bRoot] = aRoot;
            isAlive[bRoot] = false;
        } else  {
            countryPower[bRoot] += aPower;
            countryPower[aRoot] = 0;
            parent[aRoot] = bRoot;
            isAlive[aRoot] = false;
        }

    }

    private static int find(int x){
        if ( parent[x] == x ) return x;
        return parent[x] = find(parent[x]);
    }

    private static void print() {
        Collections.sort(ansList);
        System.out.println(ansList.size());
        if (!ansList.isEmpty()) {
            for (int i = 0; i < ansList.size(); i++) {
                System.out.print(ansList.get(i));
                if (i < ansList.size() - 1) System.out.print(" ");
            }
            System.out.println();
        }
    }
}
```