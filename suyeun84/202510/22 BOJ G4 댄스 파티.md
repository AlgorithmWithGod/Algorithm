```java
import java.io.*;
import java.util.*;

public class boj2831 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();
        int answer = 0;
        ArrayList<Integer> tg = new ArrayList<>();
        ArrayList<Integer> sg = new ArrayList<>();
        ArrayList<Integer> tb = new ArrayList<>();
        ArrayList<Integer> sb = new ArrayList<>();
        nextLine();
        for (int i = 0; i < N; i++) {
            int tmp = nextInt();
            if (tmp < 0) sg.add(tmp*-1);
            else tg.add(tmp);
        }
        nextLine();
        for (int i = 0; i < N; i++) {
            int tmp = nextInt();
            if (tmp < 0) sb.add(tmp*-1);
            else tb.add(tmp);
        }
        // 양수 -> 자신보다 큰, 음수 -> 자신보다 작은
        Collections.sort(tg);
        Collections.sort(sg);
        Collections.sort(tb);
        Collections.sort(sb);

        for (int i = 0, j = 0; i < tb.size() && j < sg.size();) {
            int man = tb.get(i); // 큰여자원하는남자
            int woman = sg.get(j); //작은남자원하는여자
            if (woman <= man) j++;
            else {
                i++;
                j++;
                answer++;
            }
        }
        for (int i = 0, j = 0; i < sb.size() && j < tg.size();) {
            int man = sb.get(i); //작은여자원하는남자
            int woman = tg.get(j); //큰남자원하는여자
            if (man <= woman) i++;
            else {
                i++;
                j++;
                answer++;
            }
        }
        System.out.println(answer);
    }
}
```
