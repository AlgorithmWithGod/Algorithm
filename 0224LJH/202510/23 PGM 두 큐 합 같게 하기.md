```java
import java.io.*;
import java.util.*;

class Solution {
    public int solution(int[] queue1, int[] queue2) {
        int[] arr = new int[queue1.length + queue2.length];
        int len = arr.length;
        for (int i = 0; i < queue1.length; i++){
            arr[i] = queue1[i];
        }
        for (int i = 0; i < queue2.length; i++){
            arr[queue1.length+i] = queue2[i];
        }
        
        long total = 0;
        long goal = 0;
        long cur = arr[0];
        int start = 0;
        int end = 0;
        
        for (int i = 0; i <len; i++ ) total += arr[i];
        if (total %2 != 0) return -1;
        
        goal = total/2;
        
        int answer = Integer.MAX_VALUE;
        
        while(start <= end && end < len){
            if (cur == goal) {

                if ( end < queue1.length-1){
                    answer = Math.min(answer, start + end+1 +queue2.length);
                    
                } else{
                    answer = Math.min(answer,start + end - queue1.length+1);
                }
                end++;
                if (end >= len) break;
                cur+=arr[end];
                
                
            } else if (cur < goal){
                end++;
                if (end >= len) break;
                cur+=arr[end];
            } else{
                if (arr[start] > goal) return -1;
                
                cur-=arr[start];
                start++;
            }
        }
        
        if (answer == Integer.MAX_VALUE) answer = -1;
        
        
        
        return answer;
    }
}
```
