```java
import java.io.*;
import java.util.*;

public class Main {
    static class taxi implements Comparable<taxi> {
        int start, end;
        taxi(int s, int e) {
            this.start = s;
            this.end = e;
        }
        public int compareTo(taxi o) {
            if (this.start != o.start) return Integer.compare(this.start, o.start);
            return Integer.compare(this.end, o.end);
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        List<taxi> list = new ArrayList<>();
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            if (a > b) {
                list.add(new taxi(b, a));
            }
        }

        if (list.isEmpty()) {
            System.out.println(M);
            return;
        }

        Collections.sort(list);

        long extra = 0;
        int curStart = list.get(0).start;
        int curEnd = list.get(0).end;

        for (int i = 1; i < list.size(); i++) {
            taxi t = list.get(i);
            if (t.start <= curEnd) {
                curEnd = Math.max(curEnd, t.end);
            } else {
                extra += (long)(curEnd - curStart) * 2;
                curStart = t.start;
                curEnd = t.end;
            }
        }
        extra += (long)(curEnd - curStart) * 2;

        long answer = M + extra;
        System.out.println(answer);
    }
}
```
