```java
import java.util.*;
class Solution {
    public int solution(String[] user_id, String[] banned_id) {
        HashSet<HashSet<String>> result = new HashSet<>();
        
        dfs(new HashSet<>(), user_id, banned_id, result);
        return result.size();
    }
    
    private void dfs(HashSet<String> hashset, String[] user_id, String[] banned_id, HashSet<HashSet<String>> result) {
        if (hashset.size() == banned_id.length) {
            result.add(new HashSet<>(hashset));
            return;
        };
        String target = banned_id[hashset.size()];
        
        for (String user : user_id) {
            if (hashset.contains(user)) continue;
            if (check(target, user)) {
                hashset.add(user);
                dfs(hashset, user_id, banned_id, result);
                hashset.remove(user);
            }
        }
    }
    private boolean check(String target, String user) {
        if (target.length() != user.length()) return false;
        for (int j = 0; j < target.length(); j++) {
            if (target.charAt(j) == ('*')) continue;
            if (target.charAt(j) == user.charAt(j)) continue;
            return false;
        }
        return true;
    }
}
```
