```java
import java.util.Arrays;

public class PGJ_LV2_H_Index {

    private static int len;

    public int solution(int[] citations) {
        int answer = 0;
        len = citations.length;
        Arrays.sort(citations);

        for (int i = 0; i < len; i++) {
            int h = Math.min(len - i, citations[i]);
            answer = Math.max(answer, h);
        }
        return answer;
    }

}
```