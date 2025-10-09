```java
import java.io.*;
import java.util.*;


class Solution {
    
    static int limit,houseCnt,pIdx, dIdx;
    static long totalCost;
    static House[] houses;
    
    static class House implements Comparable<House>{
        int idx;
        int delivery;
        int pickup;
        
        public House(int idx, int delivery, int pickup ){
            this.idx = idx;
            this.delivery = delivery;
            this.pickup = pickup;
        }
        
        @Override
        public int compareTo(House h){
            return Integer.compare(h.idx, this.idx); // 거리 높은순으로 나옴
        }
    }
    
    public long solution(int cap, int n, int[] deliveries, int[] pickups) {
        limit = cap;
        houseCnt = n;
        totalCost = 0;
        houses = new House[houseCnt+1];
        for (int i = 1; i<= houseCnt; i++){
            houses[i] = new House(i, deliveries[i-1], pickups[i-1]);
        }
        
        process();
        
        
        long answer = totalCost;
        return answer;
    }
    
    private void process(){
        dIdx = houseCnt;
        pIdx = houseCnt;
        
        while (dIdx != 0 || pIdx != 0){
            processEach();
        }
    }
    
    
    
    private void processEach(){
        int dLeft = limit;
        int pLeft = limit;
        
        while(dIdx != 0 && houses[dIdx].delivery == 0){
            dIdx--;
        }    
        while(pIdx != 0 && houses[pIdx].pickup == 0){
            pIdx--;
        }
        
        int curCost = Math.max(dIdx, pIdx) * 2;
        // System.out.println(curCost + " ->" + dIdx + " "+ pIdx);
        totalCost += curCost;
        
        while(dIdx != 0 && dLeft != 0){
            House h = houses[dIdx];
            if (h.delivery > dLeft){
                h.delivery -= dLeft;
                dLeft = 0;
                break;
            } 
            
            dLeft -= h.delivery;
            h.delivery = 0;
            dIdx--;
        }
        
        while(pIdx != 0 && pLeft != 0){
            House h = houses[pIdx];
            if (h.pickup > pLeft){
                h.pickup -= pLeft;
                pLeft = 0;
                break;
            } 
            
            pLeft -= h.pickup;
            h.pickup = 0;
            pIdx--;
        }        
        // System.out.println(curCost + " ->" + dIdx + " "+ pIdx);

    }
}
```
