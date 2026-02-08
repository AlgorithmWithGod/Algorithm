```java
class Solution {
    public int solution(int[] a) {
        int answer = 0;
        
        boolean[] survive = new boolean[a.length];
        
        int left = Integer.MAX_VALUE;
        
        for (int i=0; i<a.length; i++){
            if (left > a[i]){
                left = a[i];
                survive[i] = true;
            }
        }
        
        int right = Integer.MAX_VALUE;
        
        for (int i=a.length-1; i>=0; i--){
            if (right > a[i]){
                right = a[i];
                survive[i] = true;
            }
        }
        
        for (int i=0; i<a.length; i++){
            if (survive[i]) answer++;
        }
        
        return answer;
    }
}
```
