```java
class Solution {
    public int solution(String name) {
        int answer = 0;
        
        for (int i=0; i<name.length(); i++){
            int diff = name.charAt(i)-'A';
            answer += Math.min(diff, 26-diff);
        }
        
        int move = name.length()-1;
        for (int i=0; i<name.length(); i++){
            int next = i+1;
            
            while (next<name.length() && name.charAt(next)=='A'){
                next++;
            }
            
            move = Math.min(move, i*2+(name.length()-next));
            move = Math.min(move, i+(name.length()-next)*2);
        }
        
        return answer+move;
    }
}
```
