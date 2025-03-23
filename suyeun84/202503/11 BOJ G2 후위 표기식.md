```java
import java.util.*;
import java.io.*;

public class boj1918 {
	  static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringBuilder sb = new StringBuilder();
    
    public static void main(String[] args) throws Exception {
    	String input = br.readLine();
    	Stack<Character> stack = new Stack<>();
    	for (int i = 0; i < input.length(); i++) {
    		char c = input.charAt(i);
    		switch(c) {
	    		case '+':
	    		case '-':
	    		case '*':
	    		case '/':
	    			while (!stack.isEmpty() && priority(stack.peek()) >= priority(c)) {
	    				sb.append(stack.pop());
	    			}
	    			stack.add(c);
	    			break;
	    		case '(':
	    			stack.add(c);
	    			break;
	    		case ')':
	    			while (!stack.isEmpty() && stack.peek() != '(') {
	    				sb.append(stack.pop());
	    			}
	    			stack.pop();
	    			break;
	    		default:
	    			sb.append(c);
    		}
    	}
    	while (!stack.isEmpty()) {
    		sb.append(stack.pop());
    	}
    	System.out.println(sb.toString());
    }
    
    public static int priority(char op) {
    	if (op == '(' || op ==')') return 0;
    	else if (op == '+' || op == '-') return 1;
    	else if (op == '*' || op == '/') return 2;
    	return -1;
    }
}

```
