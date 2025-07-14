```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static StringBuilder sb = new StringBuilder();
    static int stuffCnt,pairCnt;
    static Stuff[] stuffs;
    static boolean[][] visited;


    static class Stuff implements Comparable<Stuff>{
        int num;
        int parentCnt = 0;
        List<Stuff> parents = new ArrayList<>();
        List<Stuff> children = new ArrayList<>();

        public Stuff(int num) {
            this.num = num;
        }

        @Override
        public int compareTo(Stuff o) {
            return o.parentCnt - this.parentCnt;
        }

        //
        public void addToChildParentList(int num) {
            for (Stuff child : children) {
                if (visited[child.num][num]) continue;
                visited[child.num][num] = true;
                child.addToChildParentList(num);
            }
        }

        public void addToParentChildList(int num) {
            for ( Stuff parent : parents) {
                if (visited[parent.num][num]) continue;
                visited[parent.num][num] = true;
                parent.addToParentChildList(num);
            }
        }
    }


    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        stuffCnt = Integer.parseInt(br.readLine());
        pairCnt = Integer.parseInt(br.readLine());

        stuffs = new Stuff[stuffCnt+1];
        visited = new boolean[stuffCnt+1][stuffCnt+1];

        for (int i = 1; i <= stuffCnt; i++) {
            stuffs[i] = new Stuff(i);
            visited[i][i] = true;
        }

        for (int i = 0; i < pairCnt; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int parent = Integer.parseInt(st.nextToken());
            int child = Integer.parseInt(st.nextToken());

            stuffs[parent].children.add(stuffs[child]);
            stuffs[child].parents.add(stuffs[parent]);
            stuffs[child].parentCnt++;
            visited[parent][child] = true;
            visited[child][parent] = true;
        }
    }

    private static void process() {
        PriorityQueue<Stuff> pq = new PriorityQueue<>();
        for (int i = 1; i <= stuffCnt; i++) {
            pq.add(stuffs[i]);
        }

        while (!pq.isEmpty()) {
            Stuff s = pq.poll();
            int num  = s.num;

            for (Stuff child : s.children) {
                child.addToChildParentList(num);
            }
            for (Stuff parent : s.parents) {
                parent.addToParentChildList(num);
            }
        }

        for (int i = 1; i <= stuffCnt; i++) {
            int ans = stuffCnt;

            for (int j = 1; j <= stuffCnt; j++) {
                if (visited[i][j]) ans--;
            }
            sb.append(ans).append("\n");
        }


    }




    private static void print()  {
        System.out.println(sb.toString());
    }



}

```