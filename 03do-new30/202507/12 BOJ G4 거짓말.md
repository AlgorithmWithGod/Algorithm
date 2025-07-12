```java
import java.io.*;
import java.util.*;

public class Main {

    static int N, M;
    static boolean[] knowingTruth;
    static int[] parents;


    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        knowingTruth = new boolean[N+1];
        Arrays.fill(knowingTruth, false);
        st = new StringTokenizer(br.readLine());
        int knowing = Integer.parseInt(st.nextToken());
        for (int i = 0; i < knowing; i++) {
            int id = Integer.parseInt(st.nextToken());
            knowingTruth[id] = true;
        }

        initParents();
        List<Integer>[] logs = new List[M];
        for (int i = 0; i < M; i++) {
            logs[i] = new ArrayList<>();
            st = new StringTokenizer(br.readLine());
            int count = Integer.parseInt(st.nextToken());
            int[] arr = new int[count];
            for (int j = 0; j < count; j++) {
                arr[j] = Integer.parseInt(st.nextToken());
                logs[i].add(arr[j]);
            }
            for (int j = 0; j < count - 1; j++) {
                for (int k = j + 1; k < count; k++) {
                    union(arr[j], arr[k]);
                }
            }
        }

        // 거짓말을 할 수 있는 파티인지 판별
        int answer = 0;
        for (int i = 0; i < M; i++) {
            boolean canLie = true;
            for (int participant : logs[i]) {
                if (knowingTruth[find(participant)]) {
                    canLie = false;
                    break;
                }
            }
            if (canLie) answer++;
        }

        System.out.println(answer);


        br.close();
    }

    private static void initParents() {
        parents = new int[N+1];
        for (int i = 1 ; i < N+1; i++) {
            parents[i] = i;
        }
    }

    private static int find(int x) {
        if (x == parents[x]) return x;
        return parents[x] = find(parents[x]);
    }

    private static boolean union(int a, int b) {
        int rootA = find(a);
        int rootB = find(b);

        if (rootA == rootB) return false;

        boolean aKnows = knowingTruth[rootA];
        boolean bKnows = knowingTruth[rootB];

        if (rootA < rootB) {
            parents[rootB] = rootA;
        } else {
            parents[rootA] = rootB;
        }
        knowingTruth[rootA] = knowingTruth[rootB] = aKnows || bKnows;
        return true;
    }
}
```
