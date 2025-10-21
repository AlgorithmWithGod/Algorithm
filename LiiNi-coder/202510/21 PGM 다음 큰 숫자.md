```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        int i = n+1;
        int n1 = get1OfBinary(n);
        while(get1OfBinary(i) != n1){
            i++;
        }
        return i;
    }
    public static int get1OfBinary(int n){
        int result = 0;
        while(n>1){
            result += n%2;
            n/=2;
        }
        if(n==1){
            result++;
        }
        return result;
    }
}
```
