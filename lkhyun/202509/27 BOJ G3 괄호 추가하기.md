```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static int N;
    static String line;
    static int max = Integer.MIN_VALUE;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        line = br.readLine();
        
        dfs(0, Integer.parseInt(String.valueOf(line.charAt(0))));
        bw.write(max+"");
        bw.close();
    }
    static void dfs(int idx, int cur) {
        
        if (idx >= N - 1) {
            max = Math.max(max, cur);
            return;
        }
        
        char operator = line.charAt(idx + 1);
        int nextNum = Integer.parseInt(String.valueOf(line.charAt(idx + 2)));
        
        int noBracket = calculate(cur, operator, nextNum);
        dfs(idx + 2, noBracket);
        
        if (idx + 4 < N) {
            char nextOperator = line.charAt(idx + 3);
            int nextNextNum = Integer.parseInt(String.valueOf(line.charAt(idx + 4)));
            
            int bracketResult = calculate(nextNum, nextOperator, nextNextNum);
            int Bracket = calculate(cur, operator, bracketResult);
            dfs(idx + 4, Bracket);
        }
    }
    static int calculate(int a, char op, int b) {
        if(op == '+'){
            return a+b;
        }else if(op == '-'){
            return a-b;
        }else if(op == '*'){
            return a*b;
        }else{
            return 0;
        }
    }
}
```
