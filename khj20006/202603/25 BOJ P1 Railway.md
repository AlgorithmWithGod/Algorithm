```java
import java.io.*;
import java.util.*;

public class BOJ22197 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static int N, M, K;
    static List<int[]>[] tree;
    static TreeMap<Integer, Integer>[] map;
    static int[] size;
    static int answerCount = 0;
    static boolean[] isAnswer;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        tree = new List[N+1];
        for(int i=1;i<=N;i++) {
            tree[i] = new ArrayList<>();
        }

        for(int i=1;i<N;i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken()), b = Integer.parseInt(st.nextToken());
            tree[a].add(new int[]{b,i});
            tree[b].add(new int[]{a,i});
        }

        map = new TreeMap[N+1];
        for(int i=1;i<=N;i++) {
            map[i] = new TreeMap<>();
        }
        size = new int[M];
        for(int i=0;i<M;i++) {
            st = new StringTokenizer(br.readLine());
            size[i] = Integer.parseInt(st.nextToken());
            for(int j=0;j<size[i];j++) {
                map[Integer.parseInt(st.nextToken())].put(i, 1);
            }
        }

        isAnswer = new boolean[N];
        dfs(1, 0);

        bw.write(answerCount + "\n");
        for(int i=1;i<N;i++) if(isAnswer[i]) {
            bw.write(i + " ");
        }

        bw.close();
    }

    public static void dfs(int cur, int par) {
        for(int[] edge : tree[cur]) {
            int nxt = edge[0], edgeNum = edge[1];
            if(nxt == par) {
                continue;
            }

            dfs(nxt, cur);
            if(map[nxt].size() >= K) {
                answerCount++;
                isAnswer[edgeNum] = true;
            }

            if(map[cur].size() < map[nxt].size()) {
                TreeMap<Integer, Integer> temp = map[cur];
                map[cur] = map[nxt];
                map[nxt] = temp;
            }

            for(int key : map[nxt].keySet()) {
                int newVal = map[cur].getOrDefault(key, 0) + map[nxt].get(key);
                if(newVal != size[key]) {
                    map[cur].put(key, newVal);
                }
                else if(map[cur].containsKey(key)) {
                    map[cur].remove(key);
                }
            }
        }
    }
}
```
