```java
import java.util.*;

class Solution {
    Map<String, Integer> map;
    int max = 0;
    
    public void dfs(String order, String key, int index, int end, int depth) {
        if(depth == end) {
            map.put(key, map.getOrDefault(key, 0) + 1);
            max = Math.max(max, map.get(key));
        }
        
        for(int i = index + 1; i < order.length(); i++) {
            dfs(order, key + order.charAt(i), i, end, depth + 1);
        }
    }
    
    public String[] solution(String[] orders, int[] course) {
        ArrayList<String> ans = new ArrayList<>();
        
        for(int c : course) {
            map = new HashMap<>();
            max = 0;
            
            for(String order: orders) {
                char[] strs = order.toCharArray();
                Arrays.sort(strs);
                order = new String(strs);
                dfs(order, "", -1, c, 0);
            }
            
            for(String key : map.keySet()) {
                int value = map.get(key);
                if(value > 1 && max == value) {
                    ans.add(key);
                }
            }
        }
        
        Collections.sort(ans);
        String[] answer = ans.toArray(new String[ans.size()]);
        
        return answer;
    }
}
```
