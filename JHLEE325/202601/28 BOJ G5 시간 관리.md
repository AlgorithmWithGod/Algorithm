```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.*;

class Job implements Comparable<Job> {
    int time;
    int end;

    public Job(int time, int end) {
        this.time = time;
        this.end = end;
    }

    @Override
    public int compareTo(Job o) {
        return o.end - this.end;
    }
}

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int N = Integer.parseInt(br.readLine());

        Job[] jobs = new Job[N];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());
            jobs[i] = new Job(start, end);
        }

        Arrays.sort(jobs);

        int currentTime = jobs[0].end;

        for (int i = 0; i < N; i++) {
            if (jobs[i].end < currentTime) {
                currentTime = jobs[i].end;
            }
            currentTime -= jobs[i].time;
        }

        if (currentTime >= 0) {
            System.out.println(currentTime);
        } else {
            System.out.println("-1");
        }
    }
}
```
