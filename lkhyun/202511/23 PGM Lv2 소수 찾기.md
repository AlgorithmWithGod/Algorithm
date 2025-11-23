```java
import java.util.*;
class Solution {
    static int[] number;
    static boolean[] visited;
    static int len;
    static Set<Integer> primes = new HashSet<>();
    
    public int solution(String numbers) {
        len = numbers.length();
        number = new int[len];
        visited = new boolean[len];
        primes.clear();
        
        for(int i = 0; i < len; i++){
            number[i] = Character.getNumericValue(numbers.charAt(i));
        }
        
        findPrime(new StringBuilder());
        return primes.size();
    }
    
    public static void findPrime(StringBuilder sb){
        if(sb.length() > 0){
            int num = Integer.parseInt(sb.toString());
            if(isPrime(num)){
                primes.add(num);
            }
        }
        
        for(int i = 0; i < len; i++){
            if(!visited[i]){
                visited[i] = true;
                sb.append(number[i]);
                findPrime(sb);
                sb.deleteCharAt(sb.length() - 1);
                visited[i] = false;
            }
        }
    }
    
    public static boolean isPrime(int num){
        if(num < 2) return false;
        if(num == 2) return true;
        if(num % 2 == 0) return false;
        
        for(int i = 3; i * i <= num; i += 2){
            if(num % i == 0) return false;
        }
        return true;
    }
}
```
