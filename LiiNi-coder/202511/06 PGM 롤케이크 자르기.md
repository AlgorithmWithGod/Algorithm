```java
import java.util.*;

class Solution {
    public int solution(int[] toppings) {
        int answer=0;
        HashMap<Integer, Integer> r = new HashMap<>();
        for(int topping: toppings){
            if(!r.containsKey(topping)){
                r.put(topping, 0);
            }
            r.put(topping, r.get(topping)+1);
        }
        HashMap<Integer, Integer> l = new HashMap<>();
        for(int topping: toppings){
            if(!l.containsKey(topping)){
                l.put(topping, 0);
            }
            l.put(topping, l.get(topping)+1);
            r.put(topping, r.get(topping)-1);
            if(r.get(topping) == 0)
                r.remove(topping);
            if(l.size() == r.size())
                answer++;
        }
        return answer;
    }
    
}
```
