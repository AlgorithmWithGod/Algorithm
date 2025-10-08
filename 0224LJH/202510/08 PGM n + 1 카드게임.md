```java
import java.io.*;
import java.util.*;

/*
결국 N+1을 내야한다면, 1~N에서 파트너를 맞춰야함. ->
결국 종료는

1. N/2라운드가 지나서 모든 카드를 다 냈거나,
2. N+1의 합을 못내서 종료

cards와 coin은 모두 1000 이하

우선 정리하자면
- N+1 합을 만드는 것 사이의 우선순위는 X
- 무조건 한 라운드에 하나씩은 만들어야함.

-> 기존에 가지고 있는 카드의 파트너라면 반드시 가져와야함.

모든 페어가, 어느 라운드에서 완성될 수 있는 지를 확인하자.
그래서 빨리 완성되는 것을 우선순위로 하여서 PQ에 넣고, 꺼내면됨.
이때 처음부터 둘 다 있었으면 -0, 하나만 있었으면 -1, 둘 다 없었으면 -2
그리고 그렇게 완성되는 라운드가, 이전에 나온 페어 개수보다 적으면 도달할 수 없으니 탈락.

*/

class Solution {
    
    static int coinLeft, cardCnt, pairCnt,curRound;
    static Pair[] pairs;
    static PriorityQueue<Pair> pq = new PriorityQueue<>();
    
    
    static class Pair implements Comparable<Pair>{
        int small,big;
        
        int minIdx = Integer.MAX_VALUE;
        int maxIdx = Integer.MIN_VALUE;
        
        public Pair(int small){
            this.small = small;
            this.big = cardCnt+1 -small;
        }
        
        public void putIdx(int idx){
            minIdx = Math.min(minIdx, idx);
            maxIdx = Math.max(maxIdx, idx);
        }
        
        public int cost(){
            if (minIdx == 0 && maxIdx == 0) return 0;
            else if (minIdx != 0 && maxIdx != 0) return 2;
            else return 1;
        }
        
        @Override
        public int compareTo(Pair p){
            if (p.maxIdx == this.maxIdx){
                return Integer.compare(this.minIdx, p.minIdx);
            }
            return Integer.compare(this.maxIdx, p.maxIdx);
        }
    }
    
    public int solution(int coin, int[] cards) {
        init(coin, cards);
        process();
        
        
        int answer = curRound;
        return answer;
    }
    
    private void process(){
        curRound = 1;
        int maxRound = pairCnt*2 / 3;
        while(curRound <= maxRound ){
            int idx = -1;
            int curCost = 3;
            for (int i =1 ; i <= pairCnt; i++){
                Pair p =pairs[i];
                if (p == null) continue;
                if (p.maxIdx > curRound) continue;
                
                int cost = p.cost();
                if (cost <= coinLeft && cost <= curCost){
                    curCost = cost;
                    idx = i;
                }
            }
            if (idx == -1) return;
            
            curRound++;
            pairs[idx] = null;
            coinLeft -= curCost;
            
        }

    }
    
    private void init(int coin, int[] cards){
        coinLeft = coin;
        cardCnt = cards.length;
        pairCnt = cardCnt/2;
        pairs = new Pair[pairCnt+1];
        
        for (int i = 1; i <= pairCnt; i++){
            pairs[i] = new Pair(i);
        }
        
        int zeroRoundCardCnt = cardCnt/3;
        int idx = 0;
        int round = 0;
        // System.out.println(zeroRoundCardCnt);
        for (int i = 0; i <  zeroRoundCardCnt; i++){
            int num = cards[idx++];
            if (num > pairCnt) num = cardCnt+1 - num;
            
            pairs[num].putIdx(0);
        }
        
        round++;
        while(idx < cardCnt){
            for (int i = 0; i < 2; i++){
                int num = cards[idx++];
                if (num > pairCnt) num = cardCnt+1 - num;
                // System.out.println(num +" "+ round);
                pairs[num].putIdx(round);
            }
            round++;
        }

        
    }
}
```
