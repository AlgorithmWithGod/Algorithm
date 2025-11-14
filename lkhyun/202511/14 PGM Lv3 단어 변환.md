```java
class Solution {
    static int answer;
    static boolean[] visited;
    
    public int solution(String begin, String target, String[] words) {
        boolean hasTarget = false;
        for(String word : words) {
            if(word.equals(target)) {
                hasTarget = true;
                break;
            }
        }
        if(!hasTarget) return 0;
        
        answer = Integer.MAX_VALUE;
        visited = new boolean[words.length];
        DFS(begin, target, words, 0);
        
        return answer == Integer.MAX_VALUE ? 0 : answer;
    }
    
    public static void DFS(String from, String target, String[] words, int depth){
        if(target.equals(from)){
            answer = Math.min(answer, depth);
            return;
        }
        
        for(int i = 0; i < words.length; i++){
            if(visited[i]) continue;
            
            if(isOneDifferent(from, words[i])){
                visited[i] = true;
                DFS(words[i], target, words, depth + 1);
                visited[i] = false;
            }
        }
    }
    
    private static boolean isOneDifferent(String word1, String word2) {
        int diff = 0;
        for(int i = 0; i < word1.length(); i++){
            if(word1.charAt(i) != word2.charAt(i)){
                diff++;
                if(diff > 1) return false;
            }
        }
        return diff == 1;
    }
}
```
