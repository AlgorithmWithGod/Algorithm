```java
import java.util.*;

public class PGM_Lv2_아날로그_시계 {

    private static final double secMin = 3600.0 / 59;
    private static final double secHour = 43200.0 / 719;

    private static int ans;
    private static double time;
    private static Set<Double> set = new HashSet<>();

    public int solution(int h1, int m1, int s1, int h2, int m2, int s2) {
        ans = 0;

        int sec1 = h1 * 60 * 60 + m1 * 60 + s1;
        int sec2 = h2 * 60 * 60 + m2 * 60 + s2;

        for (int i = 0; i * secMin <= sec2; i++) {
            time = i * secMin;
            if (sec1 <= time) {
                set.add(time);
            }
        }

        for (int i = 0; i * secHour <= sec2; i++) {
            time = i * secHour;
            if (sec1 <= time) {
                set.add(time);
            }
        }

        System.out.println("\n" + set.size());

        return set.size();
    }
}
```
