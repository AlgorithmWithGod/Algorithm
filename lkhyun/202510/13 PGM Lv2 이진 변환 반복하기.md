```java
class Solution {
    static int convertCnt = 0;
    static int zeroCnt = 0;
    public int[] solution(String s) {
        while(!s.equals("1")){
            s = convertToBinary(s);
            convertCnt++;
        }
        return new int[]{convertCnt,zeroCnt};
    }
    public String convertToBinary(String s){
        String removedZero = s.replaceAll("0","");
        int num = removedZero.length();
        zeroCnt += s.length() - num;
        StringBuilder sb = new StringBuilder();
        
        while(num > 0){
            sb.append(num%2);
            num /= 2;
        }
        return sb.reverse().toString();
    }
}
```
