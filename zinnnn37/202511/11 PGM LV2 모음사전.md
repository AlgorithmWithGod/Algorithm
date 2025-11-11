```java
import java.util.ArrayList;
import java.util.List;

public class PGM_LV2_모음사전 {

    private static final String[] vowels = {"A", "E", "I", "O", "U"};

    private static int ans;
    private static String word;
    private static List<String> words;

    private static void dfs(int depth, String tmp) {
        if (depth > 5) {
            return;
        }

        words.add(tmp);

        for (int i = 0; i < 5; i++) {
            dfs(depth + 1, tmp + vowels[i]);
        }
    }

    public int solution(String w) {
        word = w;
        words = new ArrayList<>();

        dfs(0, "");

        int len = words.size();
        for (int i = 0; i < len; i++) {
            if (words.get(i).equals(word)) {
                ans = i;
                break;
            }
        }

        return ans;
    }
}
```