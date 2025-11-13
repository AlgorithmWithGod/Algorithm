```java
import java.util.*;

public class PGM_LV2_베스트엘범 {
    
    private static int len;

    private static Map<String, Queue<Node>> order;
    private static Map<String, Integer> cnt;

    private static class Node implements Comparable<Node> {
        int id;
        int cnt;

        Node(int id, int cnt) {
            this.id = id;
            this.cnt = cnt;
        }

        @Override
        public int compareTo(Node o) {
            return Integer.compare(o.cnt, this.cnt);
        }
    }

    public int[] solution(String[] genres, int[] plays) {
        len = genres.length;

        order = new HashMap<>();
        cnt = new TreeMap<>(Collections.reverseOrder());

        for (int i = 0; i < genres.length; i++) {
            cnt.put(genres[i], cnt.getOrDefault(genres[i], 0) + plays[i]);

            order.putIfAbsent(genres[i], new PriorityQueue<>());
            order.get(genres[i]).offer(new Node(i, plays[i]));
        }

        List<String> sortedGenres = new ArrayList<>(order.keySet());
        sortedGenres.sort((a, b) -> Integer.compare(cnt.get(b), cnt.get(a)));

        List<Integer> res = new ArrayList<>();

        for (String genre : sortedGenres) {
            Queue<Node> pq = order.get(genre);

            for (int i = 0; i < 2 && !pq.isEmpty(); i++) {
                res.add(pq.poll().id);
            }
        }

        return res.stream().mapToInt(i -> i).toArray();
    }
}
```