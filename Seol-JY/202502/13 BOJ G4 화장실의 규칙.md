```java
import java.io.*;
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.List;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;
public class Main {
    public static void main(String[] args) throws IOException {
        Queue<Person> queue = new PriorityQueue<>();

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());


        List<Queue<Person>> lists = new ArrayList<>();
        for (int i = 0; i < M; i++) {
            lists.add(new ArrayDeque<>());
        }

        for (int i = 0; i < N; i++) {
            lists.get(i%M).add(Person.create(br, K, i, i%M));
        }

        int answer = 0;
        for (int i = 0; i < M; i++) {
            if(!lists.get(i).isEmpty()) queue.add(lists.get(i).poll());
        }
        while(true) {
            Person person = queue.poll();
            if (person.getIsDeka()) {
                System.out.println(answer);
                break;
            }
            answer++;

            if(!lists.get(person.getLine()).isEmpty()) {
                queue.add(lists.get(person.getLine()).poll());
            }
        }


    }

    static class Person implements Comparable<Person> {
        private final int d;
        private final int h;
        private final boolean isDeka;
        private final int line;

        private Person(int d, int h, boolean isDeka, int line) {
            this.d = d;
            this.h = h;
            this.isDeka = isDeka;
            this.line = line;
        }

        public static Person create(BufferedReader br, int k, int index, int line) throws IOException {
            StringTokenizer st = new StringTokenizer(br.readLine());
            return new Person(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()), index == k, line);
        }

        public int getLine() {
            return this.line;
        }

        public boolean getIsDeka() {
            return this.isDeka;
        }

        @Override
        public int compareTo(Person o) {
            int compareD = o.d - this.d;
            if (compareD != 0) return compareD;

            int compareH = o.h - this.h;
            if (compareH != 0) return compareH;
            
            return this.line - o.line;
        }
    }
}

```
