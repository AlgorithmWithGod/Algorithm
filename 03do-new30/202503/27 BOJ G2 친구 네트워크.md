```java
import java.io.*;
import java.util.*;

public class Main {

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static int F, cnt;
    static Map<String, Integer> map;
    static int[] parents, friends;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());
        for (int tc = 1; tc <= T; tc++) {

            F = Integer.parseInt(br.readLine());
            map = new HashMap<>();
            cnt = 0;

            makeSet();
            init();

            for (int i = 0 ; i < F; i++) {
                StringTokenizer st = new StringTokenizer(br.readLine());
                String name1 = st.nextToken();
                String name2 = st.nextToken();
                addName(name1); // 이름 관리
                addName(name2);
                union(map.get(name1), map.get(name2));
                // 두 사람의 친구 네트워크에 몇 명이 있는지 구한다.
                int root = find(map.get(name1));
                System.out.println(friends[root]);
            }
        }
        br.close();
    }

    static void addName(String name) {
        if (map.containsKey(name)) return;
        map.put(name, cnt++);
    }
    
    static void init() {
        // friends[i] = i가 집합의 대표자일 때, 해당 집합에 속하는 친구들의 수
        friends = new int[F*2];
        for (int i = 0; i < F*2; i++) {
            friends[i] = 1; // 초기에는 자기 자신만 친구...
        }
    }

    static void makeSet() {
        parents = new int[F * 2]; // F개 관계 -> 최대 F*2명의 사람 존재 가능
        for (int i = 0; i < F * 2; i++) {
            parents[i] = i;
        }
    }

    static int find(int a) {
        if (a == parents[a]) return a;
        return parents[a] = find(parents[a]);
    }

    static boolean union(int a, int b) {
        int aRoot = find(a);
        int bRoot = find(b);
        if (aRoot == bRoot) return false;
        if (aRoot < bRoot) {
            parents[bRoot] = aRoot;
            friends[aRoot] += friends[bRoot]; // 친구 수 합치깅
        } else {
            parents[aRoot] = bRoot;
            friends[bRoot] += friends[aRoot]; // 친구 수 합치깅
        }
        return true;
    }


}

```
