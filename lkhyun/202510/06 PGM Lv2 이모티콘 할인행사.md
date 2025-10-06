```java
class Solution {
    static int maxCnt = 0;
    static int maxSell = 0;
    public int[] solution(int[][] users, int[] emoticons) {
        saleCase(users, emoticons, 0, 0, new int[emoticons.length]);
        return new int[]{maxCnt,maxSell};
    }
    public void saleCase(int[][] users, int[] emoticons, int start, int count, int[] selected){
        if(count == emoticons.length){
            int curCnt = 0;
            int curSell = 0;
            int[] adaption = adaptSale(emoticons,selected);
            for(int[] user : users){
                int userTotal = 0;
                for(int i=0;i<count;i++){
                    if(selected[i] >= user[0]){
                        userTotal += adaption[i];
                    }
                }
                if(userTotal >= user[1]){
                    curCnt++;
                }else{
                    curSell += userTotal;
                }
            }
            if(maxCnt < curCnt){
                maxCnt = curCnt;
                maxSell = curSell;
            }else if(maxCnt == curCnt){
                maxSell = Math.max(maxSell,curSell);
            }
            return;
        }
        
        for(int i=1;i<=4;i++){
            selected[start] = i*10;
            saleCase(users,emoticons,start+1,count+1,selected);
        }
    }
    public int[] adaptSale(int[] price, int[] rate){
        int[] adaption = new int[price.length];
        for(int i=0;i<adaption.length;i++){
            adaption[i] = (price[i]*(100-rate[i]))/100;
        }
        return adaption;
    }
}
```
