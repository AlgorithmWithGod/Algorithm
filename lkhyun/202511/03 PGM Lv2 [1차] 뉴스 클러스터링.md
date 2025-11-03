```java
import java.util.*;

class Solution {
    public int solution(String str1, String str2) {
        List<String> A = new ArrayList<>();
        List<String> B = new ArrayList<>();
        
        for(int i = 0; i + 1 < str1.length(); i++){
            String temp = str1.substring(i, i + 2);
            if(!validation(temp.charAt(0)) || !validation(temp.charAt(1))) continue;
            A.add(temp.toLowerCase());
        }

        for(int i = 0; i + 1 < str2.length(); i++){
            String temp = str2.substring(i, i + 2);
            if(!validation(temp.charAt(0)) || !validation(temp.charAt(1))) continue;
            B.add(temp.toLowerCase());
        }
        
        if(A.isEmpty() && B.isEmpty()) {
            return 65536;
        }
        
        Collections.sort(A);
        Collections.sort(B);
        
        int intersection = 0;
        int a = 0;
        int b = 0;
        while(a < A.size() && b < B.size()){
            int compare = A.get(a).compareTo(B.get(b));
            if(compare == 0){
                intersection++;
                a++;
                b++;
            } else if(compare < 0){
                a++;
            } else {
                b++;
            }
        }
        
        int union = A.size() + B.size() - intersection;
        
        return (int)((double)intersection / union * 65536);
    }
    
    public boolean validation(char c){
        return (c >= 'A' && c <= 'Z') || (c >= 'a' && c <= 'z');
    }
}
```
