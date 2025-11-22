```java
class Solution {
    public int solution(int n, int[] stations, int w) {
        int answer = 0;
        
        int idx = 1;
        for(int station : stations){
            if(idx < station - w){
                answer += install(idx,station-w-1,w);
            }
            idx = station+w+1;
            if(station+w >= n) break;
        }
        if(idx <= n){
            answer += install(idx,n,w);
        }

        return answer;
    }
    public int install(int start, int end, int w){
        int range = end - start + 1;
        int size = w*2 + 1;
        return range%size != 0 ? range/size + 1 : range/size;
    }
}
```
