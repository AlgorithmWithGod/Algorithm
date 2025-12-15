```java
import java.util.*;

class Solution {
    private static final char[] VOWELS = {'A','E','I','O','U'};
    private static List<String> dict;

    public int solution(String word) {
        dict = new ArrayList<>();
        dfs("");

        for(int i = 0; i < dict.size(); i++){
            if(dict.get(i).equals(word)){
                return i + 1;
            }
        }
        return 0;
    }

    private void dfs(String cur){
        if(cur.length() > 0){
            dict.add(cur);
        }
        if(cur.length() == 5){
            return;
        }

        for(int i = 0; i < 5; i++){
            dfs(cur + VOWELS[i]);
        }
    }
}

```
