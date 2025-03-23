```java
import java.io.*;
import java.util.ArrayDeque;

public class Main {
    static ArrayDeque<Character> stack = new ArrayDeque<>();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        String userInput = br.readLine();

        for (int i = 0; i < userInput.length(); i++) {
            char target = userInput.charAt(i);

            switch(target) {
                case '+':
                case '-':
                case '*':
                case '/':
                    while (!stack.isEmpty() && priority(stack.peek()) >= priority(target)) {
                        sb.append(stack.pop());
                    }
                    stack.push(target);
                    break;
                case '(':
                    stack.push(target);
                    break;
                case ')':
                    while (!stack.isEmpty() && stack.peek() != '(') {
                        sb.append(stack.pop());
                    }
                    stack.pop();
                    break;
                default:
                    sb.append(target);
            }
        }
        
        while (!stack.isEmpty()) {
            sb.append(stack.pop());
        }
        
        System.out.println(sb.toString());
    }

    public static int priority(char op) {
        if (op == '(' || op ==')') return 0;
        if (op == '+' || op == '-') return 1;
        if (op == '*' || op == '/') return 2;
        return -1;
    }
}
```
