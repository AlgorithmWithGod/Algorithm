```java
import java.util.*;
class Solution {
    private static List<int[]> combs;
    private static int[] comb;
    private static int[] coupons = new int[]{10, 20, 30, 40};
    private static int NOfE;
    public int[] solution(int[][] users, int[] emoticons) {
        NOfE = emoticons.length;
        combs = new LinkedList<int[]>();
        comb = new int[NOfE];
        var answer1 = 0;
        var answer2 = 0;
        //# 이모티콘 부분집합 for ex. 10, 20, 30, 30, 30... 4^7
        getComb();
        for(int[] combE : combs){
            //System.out.println(Arrays.toString(combE));
            int[] candidates = new int[2];
        //## 유저 for문
            int[] prices = new int[NOfE];
            for(int i = 0; i<prices.length; i++)
                prices[i] = emoticons[i]/100 * (100 - combE[i]);
            outer:
            for(int[] u: users){
                //System.out.println(Arrays.toString(u));
                int uPercent = u[0];
                int uPrice = u[1];
                int uTotal = 0;
                for(int i = 0; i<combE.length; i++){
                    int percent = combE[i];
                    if(percent < uPercent)
                        continue;
                    uTotal += prices[i];
                    //System.out.println(uTotal);
                    if(uTotal >= uPrice){
                        //System.out.println("넘음!");
                        candidates[0] += 1;
                        continue outer;
                    }
                }
                candidates[1] += uTotal;
            }
            //System.out.println(String.format("중간결과: %d %d", candidates[0], candidates[1]));
            boolean b1 = answer1 <= candidates[0];
            boolean b2 = answer2 <= candidates[1];
            if(answer1 == candidates[0]){
                if(answer2 <= candidates[1]){
                    answer2 = candidates[1];
                }
            }else if(answer1 < candidates[0]){
                answer1 = candidates[0];
                answer2 = candidates[1];
            }
                
        //###     
        }
        
        return new int[]{answer1, answer2};
    }
    private void getComb(){
        dfs(0);
    }
    private void dfs(int index){
        if(index == NOfE){
            combs.add(comb.clone());
            return;
        }
        for(int coupon: coupons){
            comb[index] = coupon;
            dfs(index+1);
        }
    }
}
```
