```java
import java.io.*;
import java.util.*;

public class Main {
    static int N;
    static String expression;
    static int maxResult = Integer.MIN_VALUE;
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        expression = br.readLine();
        
        if (N == 1) {
            System.out.println(expression.charAt(0) - '0');
            return;
        }
        
        dfs(0, expression.charAt(0) - '0');
        System.out.println(maxResult);
    }
    
    static void dfs(int idx, int currentValue) {
        if (idx >= N - 1) {
            maxResult = Math.max(maxResult, currentValue);
            return;
        }
        
        char operator = expression.charAt(idx + 1);
        int nextNum = expression.charAt(idx + 2) - '0';
        
        int nextValue = calculate(currentValue, operator, nextNum);
        dfs(idx + 2, nextValue);
        
        if (idx + 4 < N) {
            char nextOperator = expression.charAt(idx + 3);
            int nextNextNum = expression.charAt(idx + 4) - '0';
            
            int bracketResult = calculate(nextNum, nextOperator, nextNextNum);
            int resultWithBracket = calculate(currentValue, operator, bracketResult);
            dfs(idx + 4, resultWithBracket);
        }
    }
    
    static int calculate(int a, char operator, int b) {
        switch (operator) {
            case '+': return a + b;
            case '-': return a - b;
            case '*': return a * b;
            default: return 0;
        }
    }
}
```
