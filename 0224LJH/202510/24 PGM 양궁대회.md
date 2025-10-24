```java
import java.io.*;
import java.util.*;

class Solution {
    // 각 과녁판 점수를 얻냐, 못얻냐 -> 2^10 == 1024가지. 다 해보면 끝.
    static boolean[] win = new boolean[11];
    static int[] ans = {-1};
    static int largestDiff = 0;
    static int total;
    static int[] target;
    
    
    public int[] solution(int n, int[] info) {
        total = n;
        int[] answer = {};
        target = info;
        doRecursive(0);
        answer = ans;
        return answer;
    }
    
    public void doRecursive(int num){
        if (num == 11){
            process();
            return;
        }
        
        win[num] = true;
        doRecursive(num+1);
        win[num] = false;
        doRecursive(num+1);
    }
    
    
    public void process(){
        int[] curArr = new int[11];
        int curLeft = total;
        int pointDiff = 0;
        
        for (int i = 0; i < 10; i++){
            int point = 10 - i;
            int minimum = target[i]+1;
            if (!win[i]) {
                if(target[i] != 0) pointDiff -= point;
                continue;
            }
            if (curLeft < minimum)return;
            curArr[i] = minimum;
            curLeft -= minimum;
            pointDiff += point;
            
        }
        curArr[10] = curLeft;
        
        if (pointDiff > largestDiff){
            largestDiff = pointDiff;
            ans = curArr;
            return;
        }
        
        if (pointDiff != 0 && pointDiff == largestDiff){
            for (int i = 10; i >= 0; i--){
                if (ans[i] == curArr[i]) continue;
                if (ans[i] < curArr[i]) ans = curArr;
                else return;
            }
            
        }
    }
}
```
