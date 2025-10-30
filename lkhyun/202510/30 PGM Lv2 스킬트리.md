```java
import java.util.*;
class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;
        List<Integer>[] adjList = new List[26];
        for(int i = 0; i<26; i++){
            adjList[i] = new ArrayList<>();
        }
        int[] degree = new int[26];
        
        for(int i = 0; i<skill.length(); i++){
            for(int j = i+1; j<skill.length(); j++){
                adjList[skill.charAt(i) - 'A'].add(skill.charAt(j) - 'A');
                degree[skill.charAt(j) - 'A']++;
            }
        }
        
        for(String s : skill_trees){
            int[] temp = degree.clone();
            boolean flag = true;
            for(int i = 0;i<s.length(); i++){
                if(temp[s.charAt(i) - 'A'] != 0){
                    flag = false;
                    break;
                }
                for(int a : adjList[s.charAt(i) - 'A']){
                    temp[a]--;
                }
            }
            if(flag) answer++;
        }
        return answer;
    }
}
```
