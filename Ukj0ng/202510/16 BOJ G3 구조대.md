```
import java.io.*;
import java.util.*;

public class Main {
    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<int[]> events;
    private static Map<Integer, Integer> teamCount;
    private static int N, M;
    public static void main(String[] args) throws IOException {
        init();
        int answer = solve();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        events = new ArrayList<>();

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int l = Integer.parseInt(st.nextToken());
            int r = Integer.parseInt(st.nextToken());
            int team = Integer.parseInt(st.nextToken());

            int startS = Math.max(0, l-M);
            int endS = r;

            events.add(new int[]{startS, 0, team});
            events.add(new int[]{endS, 1, team});
        }

        Collections.sort(events, (o1, o2) -> Integer.compare(o1[0], o2[0]));

        teamCount = new HashMap<>();
    }

    private static int solve() {
        int answer = 0;
        int prevS = -1;
        int validTeams = 0;

        for (int[] element : events) {
            if (element[0] != prevS && prevS >= 0) {
                answer = Math.max(answer, validTeams);
            }

            int team = element[2];
            int oldCount = teamCount.getOrDefault(team, 0);

            if (element[1] == 0) {
                int newCount = oldCount + 1;
                teamCount.put(team, newCount);

                if (oldCount == 1 && newCount == 2) {
                    validTeams++;
                }
            } else {
                int newCount = oldCount - 1;

                if (oldCount == 2 && newCount == 1) {
                    validTeams--;
                }

                if (newCount == 0) {
                    teamCount.remove(team);
                } else {
                    teamCount.put(team, newCount);
                }
            }

            prevS = element[0];
        }

        answer = Math.max(answer, validTeams);
        return answer;
    }
}
```
