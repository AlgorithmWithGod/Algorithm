```java
class Solution {
    public String solution(String s) {
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        String[] splited = s.split(" ");
        
        int idx = 0;
        for(String n : splited){
            int num = Integer.parseInt(n);
            min = Math.min(min, num);
            max = Math.max(max, num);
        }
        return min + " " + max;
    }
}
```
