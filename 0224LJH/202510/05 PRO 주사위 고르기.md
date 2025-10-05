```java
import java.io.*;
import java.util.*;
    //10C2 라고 해봤자 45임.-> 모든 경우를 다 시도해볼 수 있는 것.
    // 특정 케이스에서, sum[i]를 통해서 주사위의 합이 i가 되는게 몇번 있는 지 확인
    // 이걸 확인한 후, 상대방의 sum[]에서 이게 어디쯤 위치하는 지를 확인. 
    // 확인 시 상대방의 sum[1]부터 해서 누적합식으로 승/무/패를 적립하면 됨. 굿.
    
    // 예를 들어 mySum[300]을 구하는거면 counterSum[]의 0~299의 합은 승리수 , counterSum[300]은 무승부 수, 
    // 전체에서 저 둘을 뺀 값을 패배수가 됨. 
    // 전체는 이렇게하면 최악의 경우 한쪽 합이 6^5 == 7500?쯤 되는데, 이걸로 진행하면 문제 없다. 
    // 한번 완탐에 결국 n -> 7500*45 정도 -> 무난.

class Solution {
    
    static double maxWinRate = 0.0;
    static int[] ans;
    static Dice[] dices;
    static Dice[] mine;
    static Dice[] rival;
    
    static int diceCnt,halfCnt;
    static HashSet<Dice> combSet;
    
    static class Dice{
        int idx;
        int[] nums= new int[6];
        public Dice(int idx, int[] arr){
            this.idx = idx;
            nums = arr;
        }
    }
    
    
    
    public int[] solution(int[][] dice) {
        diceCnt = dice.length;
        halfCnt = diceCnt/2;
        dices = new Dice[diceCnt];
        
        mine = new Dice[halfCnt];
        rival = new Dice[halfCnt];
        ans = new int[halfCnt];
        combSet = new HashSet<>();
        
        for (int i = 0; i < diceCnt; i++){
            int[] input = dice[i];
            dices[i] = new Dice(i, input);
        }
        
        processCombination();
        
        return ans;
    }
    
    private void calculate(){
        int[] myResult = getSumArr(mine);
        int[] rivalResult = getSumArr(rival);
        
        long rTotal = 0;
        for (int i = 0; i <= 600; i++)rTotal += rivalResult[i];
            
        double win = 0;
        double draw = 0;
        double lose = 0;
        int rCumulSum = 0;
        
        for (int i = 0 ; i <= 600; i++){
            rCumulSum += rivalResult[i];
            
            if (myResult[i] == 0) continue;
            
            int cur = myResult[i];
            int rivalCur = rivalResult[i];
            
            win += (rCumulSum - rivalCur) * cur;
            draw += (rivalCur) * cur;
            lose += (rTotal - rCumulSum) * cur;
            
        }
        
        double winRate = win / (win+draw+lose);
        if (winRate > maxWinRate){
            for (int i = 0; i < halfCnt; i++){
                ans[i] = mine[i].idx+1;
                // System.out.print(mine[i].idx + " ");
            }
            // System.out.println (" -> "+ win + " " + draw + " "+ lose);
            maxWinRate = winRate;
        }
        
        
    }
    
    
    private int[] getSumArr(Dice[] d){
        int[] dp = new int[601];
        int[] ex = new int[601];
        ex[0] = 1;
        
        for (int tr = 0; tr < halfCnt; tr++){
            for (int i =0; i <= 600; i++){
                if (ex[i] != 0){
                    for (int j = 0; j < 6; j++){
                        if ( i + d[tr].nums[j] <= 600) dp[i+d[tr].nums[j]] += ex[i];
                    }
                }
            }
            
            ex = dp;
            dp = new int[601];
        }
        
        return ex;
        
    }
    
    private void makeDiceArr(){
        int idx = 0;
        int rIdx = 0;
        for (int i = 0 ; i < diceCnt; i++){
            if (combSet.contains(dices[i])){
                mine[idx++] = dices[i];
            } else{
                rival[rIdx++] = dices[i];
            }
        }
    }
    
    
    
    private void combination(int curSize, int idx){
        if ( curSize == halfCnt){
            makeDiceArr();
            calculate();
            return;
        }
        
        for (int i = idx+1; i < diceCnt; i++){
            combSet.add(dices[i]);
            combination(curSize+1,i);
            combSet.remove(dices[i]);
        }    
    }
    
    private void processCombination(){
        combination(0,-1);
    }
    

    
    
    
    
    
}
```
