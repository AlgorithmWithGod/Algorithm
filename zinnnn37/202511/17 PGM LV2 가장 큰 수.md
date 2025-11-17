```java
import java.util.Arrays;

public class PGM_LV2_가장_큰_수 {

    private static int len;
    private static String answer;
    private static String[] nums;

    public String solution(int[] numbers) {
        answer = "";
        len = numbers.length;
        nums = new String[len];

        for (int i = 0; i < len; i++) {
            nums[i] = String.valueOf(numbers[i]);
        }
        Arrays.sort(nums, (a, b) -> (b + a).compareTo(a + b));

        if (nums[0].equals("0")) return "0";

        for (int i = 0; i < len; i++) {
            answer += nums[i];
        }
        return answer;
    }

}
```