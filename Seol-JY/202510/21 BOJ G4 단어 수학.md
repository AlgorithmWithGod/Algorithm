```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        
        Map<Character, Integer> weights = new HashMap<>();
        
        for (int i = 0; i < n; i++) {
            String word = br.readLine();
            int len = word.length();
            for (int j = 0; j < len; j++) {
                char c = word.charAt(j);
                int weight = (int) Math.pow(10, len - 1 - j);
                weights.put(c, weights.getOrDefault(c, 0) + weight);
            }
        }
        
        List<Integer> weightList = new ArrayList<>(weights.values());
        weightList.sort((a, b) -> b - a);
        
        int result = 0;
        int digit = 9;
        for (int weight : weightList) {
            result += weight * digit;
            digit--;
        }
        
        System.out.println(result);
    }
}
```
