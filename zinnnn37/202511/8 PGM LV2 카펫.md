```java
public class PGM_LV2_카펫 {

    public int[] solution(int B, int Y) {
        int mul = B + Y;
        int sum = (B + 4) / 2;

        int sqrt = (int) Math.sqrt(sum * sum - 4 * (B + Y));

        int a = (sum + sqrt) / 2;
        int b = (sum - sqrt) / 2;

        return new int[] { a, b };
    }
}
```