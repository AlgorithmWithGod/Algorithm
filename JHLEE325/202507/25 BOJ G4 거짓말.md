```java
import java.io.*;
import java.util.*;

public class Main {
    static int[] parent;
    static boolean[] truth;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        parent = new int[n + 1];
        truth = new boolean[n + 1];
        for (int i = 1; i <= n; i++) parent[i] = i;

        st = new StringTokenizer(br.readLine());
        int t = Integer.parseInt(st.nextToken());
        List<Integer> truthList = new ArrayList<>();
        for (int i = 0; i < t; i++) {
            int person = Integer.parseInt(st.nextToken());
            truth[person] = true;
            truthList.add(person);
        }

        List<List<Integer>> parties = new ArrayList<>();

        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int cnt = Integer.parseInt(st.nextToken());
            List<Integer> party = new ArrayList<>();

            if (cnt > 0) {
                int first = Integer.parseInt(st.nextToken());
                party.add(first);
                for (int j = 1; j < cnt; j++) {
                    int next = Integer.parseInt(st.nextToken());
                    union(first, next);
                    party.add(next);
                }
            }
            parties.add(party);
        }

        Set<Integer> truthRoots = new HashSet<>();
        for (int i = 1; i <= n; i++) {
            if (truth[i]) {
                truthRoots.add(find(i));
            }
        }

        int answer = 0;
        for (List<Integer> party : parties) {
            boolean canLie = true;
            for (int person : party) {
                if (truthRoots.contains(find(person))) {
                    canLie = false;
                    break;
                }
            }
            if (canLie) answer++;
        }

        System.out.println(answer);
    }

    static int find(int x) {
        if (x != parent[x]) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }

    static void union(int a, int b) {
        int ra = find(a);
        int rb = find(b);
        if (ra != rb) {
            parent[rb] = ra;
        }
    }
}

```
