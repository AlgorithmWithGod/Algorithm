```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.*;

public class Main {

    static List<Deque<Integer>> wheel = new ArrayList<>();

    public static void rotate(int idx, int dir) {
        if (dir == 1) {
            int last = wheel.get(idx).pollLast();
            wheel.get(idx).addFirst(last);
        } else {
            int first = wheel.get(idx).pollFirst();
            wheel.get(idx).addLast(first);
        }
    }

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        for (int i = 0; i < 4; i++) {
            String line = br.readLine();
            Deque<Integer> dq = new LinkedList<>();
            for (char c : line.toCharArray()) {
                dq.add(c - '0');
            }
            wheel.add(dq);
        }

        int k = Integer.parseInt(br.readLine());

        for (int i = 0; i < k; i++) {
            st = new StringTokenizer(br.readLine());
            int num = Integer.parseInt(st.nextToken()) - 1;
            int dir = Integer.parseInt(st.nextToken());

            int[] dirs = new int[4];
            dirs[num] = dir;

            // 왼쪽
            for (int j = num; j > 0; j--) {
                int left = ((LinkedList<Integer>) wheel.get(j - 1)).get(2);
                int right = ((LinkedList<Integer>) wheel.get(j)).get(6);
                if (left != right) {
                    dirs[j - 1] = -dirs[j];
                } else {
                    break;
                }
            }

            // 오른쪽
            for (int j = num; j < 3; j++) {
                int left = ((LinkedList<Integer>) wheel.get(j)).get(2);
                int right = ((LinkedList<Integer>) wheel.get(j + 1)).get(6);
                if (left != right) {
                    dirs[j + 1] = -dirs[j];
                } else {
                    break;
                }
            }

            for (int j = 0; j < 4; j++) {
                if (dirs[j] != 0) {
                    rotate(j, dirs[j]);
                }
            }
        }

        int score = 0;
        for (int i = 0; i < 4; i++) {
            if (wheel.get(i).peekFirst() == 1) {
                score += (1 << i);
            }
        }
        System.out.println(score);
    }
}

```
