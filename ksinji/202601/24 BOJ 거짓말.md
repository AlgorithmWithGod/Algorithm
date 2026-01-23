```java
import java.io.*;
import java.util.*;

public class Main {
    static int n, m;
    static int[] parent;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        parent = new int[n + 1];
        for (int i = 1; i <= n; i++) parent[i] = i;

        st = new StringTokenizer(br.readLine());
        int truthCnt = Integer.parseInt(st.nextToken());
        int[] truth = new int[truthCnt];
        for (int i = 0; i < truthCnt; i++) {
            truth[i] = Integer.parseInt(st.nextToken());
        }

        if (truthCnt == 0) {
            for (int i = 0; i < m; i++) {
                br.readLine();
            }
            System.out.println(m);
            return;
        }

        for (int i = 1; i < truthCnt; i++) {
            union(truth[0], truth[i]);
        }

        int[][] party = new int[m][];
        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int k = Integer.parseInt(st.nextToken());
            int[] member = new int[k];
            for (int j = 0; j < k; j++) {
                member[j] = Integer.parseInt(st.nextToken());
            }
            party[i] = member;

            for (int j = 1; j < k; j++) {
                union(member[0], member[j]);
            }
        }

        int truthGroup = find(truth[0]);
        int ans = 0;

        for (int i = 0; i < m; i++) {
            boolean ok = true;
            for (int person : party[i]) {
                if (find(person) == truthGroup) {
                    ok = false;
                    break;
                }
            }
            if (ok) ans++;
        }

        System.out.println(ans);
    }

    static int find(int x) {
        if (parent[x] == x) return x;
        return parent[x] = find(parent[x]);
    }

    static void union(int a, int b) {
        a = find(a);
        b = find(b);
        if (a == b) return;
        parent[b] = a;
    }
}

```
