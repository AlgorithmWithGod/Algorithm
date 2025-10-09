```java
class Solution {
    public int solution(int n, int k) {
        int answer = 0;
        String[] numbers = convertor(n,k).split("0+");
        for(String num : numbers){
            if(!num.isEmpty() && isPrime(Long.parseLong(num))){
                answer++;
            }
        }
        return answer;
    }
    public String convertor(int n, int k){
        StringBuilder sb = new StringBuilder();
        
        while(n > 0){
            sb.append(n%k);
            n /= k;
        }
        return sb.reverse().toString();
    }
    public boolean isPrime(long number){
        if(number == 1) return false;
        if(number == 2) return true;
        if(number%2 == 0) return false;
        for(long i=3; i*i <= number; i+=2){
            if(number%i == 0){
                return false;
            }
        }
        return true;
    }
}
```
