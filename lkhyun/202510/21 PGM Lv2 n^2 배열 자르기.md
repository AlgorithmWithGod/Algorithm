```java
class Solution {
    public long[] solution(int n, long left, long right) {
        long[] answer = new long[(int)(right-left+1)];
        
        int idx = 0;
        for(long i = left; i<=right; i++,idx++){
            long ii = i/n;
            long jj = i%n;
            if(ii>=jj){
                answer[idx] = ii+1;
            }else{
                answer[idx] = jj+1;
            }
        }
        return answer;
    }
}
```
