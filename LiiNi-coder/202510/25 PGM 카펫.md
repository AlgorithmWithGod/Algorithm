```java
class Solution {
    public int[] solution(int brown, int yellow) {
        int[] answer = new int[2];
        int area = brown + yellow;
        for(int r = area/3; r>=3; r--){
            if(area % r == 0){
                int c = area / r;
                System.out.println(r + "," + c);
                if(2*c + (r-2)*2 == brown){
                    System.out.println("FIND");
                    answer[0] = c;
                    answer[1] = r;
                }
            }
        }
        return answer;
    }
}
```
