```java
class Solution {
    static final int MAX_EMOTICON = 7;
    static int MAX_USER = 0;
    static int MAX_PRICE = 0;
    static int[] discountRate = new int[MAX_EMOTICON];

    public int[] solution(int[][] users, int[] emoticons) {

        setDiscountRate(0,users, emoticons);
        int[] answer = {MAX_USER ,MAX_PRICE};
        return answer;
    }

    public void setDiscountRate(int curIdx, int[][] users, int[] emoticons) {
        if(curIdx == emoticons.length) {
            calcPrice(users,emoticons);
            return;
        }
        for(int i = 10; i<= 40 ; i+=10) {
            discountRate[curIdx] = i;
            setDiscountRate(curIdx+1, users, emoticons);
        }
    }

    public void calcPrice(int[][] users, int[] emoticons) {

        int emoticonPlus=0;
        int emoticonPrice=0;

        for(int[] user : users) {
            int price=0;
            int userDiscountRate = user[0];
            int userPlusPrice = user[1];
            for(int idx=0; idx<emoticons.length; idx++) {
                if(discountRate[idx] >= userDiscountRate) {
                    price += (emoticons[idx]/100) * (100-discountRate[idx]); 
                }
            }
            if(price >= userPlusPrice) {
                emoticonPlus++;
            } else {
                emoticonPrice += price;
            }
        }

        if(emoticonPlus > MAX_USER) {
            MAX_USER = emoticonPlus;
            MAX_PRICE = emoticonPrice;
        } 
        else if ( emoticonPlus == MAX_USER && emoticonPrice >= MAX_PRICE)   MAX_PRICE = emoticonPrice;
    }
}
```
