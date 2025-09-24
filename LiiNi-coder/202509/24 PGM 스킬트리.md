```java
import java.util.*; 

class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;
        
        int[] alphabetIndexes = new int[26];
        
        char[] cskill = skill.toCharArray();
        for(int i = 1; i<skill.length()+1; i++)
            alphabetIndexes[cskill[i-1] - 'A'] = i;
        
        for(String skill_tree: skill_trees){
            int iSkill = 1;
            boolean isCount = true;
            for(char c: skill_tree.toCharArray()){
                int cAtIndex = alphabetIndexes[c-'A'];
                if(cAtIndex == 0)
                    continue;
                if(cAtIndex != iSkill){
                    isCount = false;
                    break;
                }
                    
                iSkill++;
            }
            if(isCount)
                answer++;
        }
        return answer;
    }
}
```
