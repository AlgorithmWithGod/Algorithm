```java
class Solution {
    public int solution(int n) {
        return pibo(n);
    }
    public static int pibo(int n){
        if(n == 0)
            return 0;
        else if(n == 1)
            return 1;
        return pibo(n-1) + pibo(n-2);
    }
}
```
