```java
class Solution {
    static final char[] V = {'A','E','I','O','U'};
    static int answer = 0;
    static boolean equal = false;
    
    void dfs(String cur, String target){
        if (equal) return;
        if (!cur.isEmpty()){
            answer++;
            
            if (cur.equals(target)){
                equal = true;
                return;
            }
        }
        if (cur.length() == 5) return;
        for (char c : V){
            dfs(cur+c, target);
        }
    }
    
    public int solution(String word) {
        dfs("", word);           
        return answer;
    }
}
```
