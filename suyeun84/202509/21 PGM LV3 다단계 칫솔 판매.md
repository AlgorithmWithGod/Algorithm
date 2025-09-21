```java
import java.util.*;
class Solution {
    static Map<String,Integer> map = new HashMap();
    static Map<String,String> recommand = new HashMap();
    public int[] solution(String[] enroll, String[] referral, String[] seller, int[] amount) {
        int[] count = new int[enroll.length];
        
        for(int i =0; i<enroll.length;i++){
            map.put(enroll[i],0);
            recommand.put(enroll[i],referral[i]);
        }
        
        for(int i=0; i<seller.length; i++){
            dfs(seller[i],amount[i]*100);
        }
        
        for(int i=0; i<enroll.length;i++){
            count[i] = map.get(enroll[i]);
        }
        
        return count;

    }
    
    public static void dfs(String name, int income){
        if(name.equals("-") || income==0){
            return;
        }
        
        int parents = income/10; 
        int mine =   income-parents;
        String next = recommand.get(name);
        map.replace(name,map.get(name)+mine);
        dfs(next,parents);
    }
}
```
