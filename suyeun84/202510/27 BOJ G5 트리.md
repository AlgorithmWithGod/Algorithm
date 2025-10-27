```java
import java.io.*;
import java.util.*;

public class boj1068 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();
        int answer = 0;
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        nextLine();
        for (int i = 0; i < N; i++) graph.add(new ArrayList<Integer>());
        for (int i = 0; i < N; i++) {
            int par = nextInt();
            if (par == -1) continue;
            graph.get(par).add(i); // 부모에 자식 연결
        }
        nextLine();
        int remove = nextInt();
        boolean[] poss = new boolean[N];
        Arrays.fill(poss, true);
        Queue<Integer> q = new LinkedList<>();
        poss[remove] = false;
        for (int n : graph.get(remove)) {
            q.add(n);
            poss[n] = false;
        }
        while (!q.isEmpty()) {
            int node = q.poll();
            for (int ne : graph.get(node)) {
                if (!poss[ne]) continue;
                q.add(ne);
                poss[ne] = false;
            }
        }
        for (int i = 0; i < N; i++) {
            boolean flag = false;
            if (!poss[i]) continue;
            for (int p : graph.get(i)) {
                if (poss[p]) {
                    flag = true;
                    break;
                }
            }
            if (graph.get(i).isEmpty()) flag = false;
            if (!flag) answer++;
        }
        System.out.println(answer);
    }
}
```
