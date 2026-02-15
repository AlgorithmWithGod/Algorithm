```java
import java.io.*;
import java.util.*;

class Tree implements Comparable<Tree> {
    int r, c, age;

    public Tree(int r, int c, int age) {
        this.r = r;
        this.c = c;
        this.age = age;
    }

    @Override
    public int compareTo(Tree o) {
        return this.age - o.age;
    }
}

public class Main {

    static int N, M, K;
    static int[][] map, A;
    static Deque<Tree> trees = new ArrayDeque<>();
    static int[] dr = {-1, -1, -1, 0, 0, 1, 1, 1};
    static int[] dc = {-1, 0, 1, -1, 1, -1, 0, 1};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        map = new int[N + 1][N + 1];
        A = new int[N + 1][N + 1];

        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= N; j++) {
                A[i][j] = Integer.parseInt(st.nextToken());
                map[i][j] = 5;
            }
        }

        List<Tree> initialTrees = new ArrayList<>();
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int r = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());
            int age = Integer.parseInt(st.nextToken());
            initialTrees.add(new Tree(r, c, age));
        }
        Collections.sort(initialTrees);
        for (Tree t : initialTrees) trees.add(t);

        for (int k = 0; k < K; k++) {
            solve();
        }

        System.out.println(trees.size());
    }

    static void solve() {
        Deque<Tree> aliveTrees = new ArrayDeque<>();
        List<Tree> deadTrees = new ArrayList<>();

        while (!trees.isEmpty()) {
            Tree t = trees.pollFirst();
            if (map[t.r][t.c] >= t.age) {
                map[t.r][t.c] -= t.age;
                t.age++;
                aliveTrees.addLast(t);
            } else {
                deadTrees.add(t);
            }
        }

        for (Tree t : deadTrees) {
            map[t.r][t.c] += t.age / 2;
        }

        Deque<Tree> nextYearTrees = new ArrayDeque<>();
        for (Tree t : aliveTrees) {
            if (t.age % 5 == 0) {
                for (int i = 0; i < 8; i++) {
                    int nr = t.r + dr[i];
                    int nc = t.c + dc[i];
                    if (nr >= 1 && nr <= N && nc >= 1 && nc <= N) {
                        nextYearTrees.addFirst(new Tree(nr, nc, 1));
                    }
                }
            }
        }

        for (Tree t : aliveTrees) {
            nextYearTrees.addLast(t);
        }
        trees = nextYearTrees;

        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= N; j++) {
                map[i][j] += A[i][j];
            }
        }
    }
}
```
