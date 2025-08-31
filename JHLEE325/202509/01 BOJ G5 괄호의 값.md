```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();

        Stack<Character> stack = new Stack<>();
        Stack<Integer> values = new Stack<>();

        for (int i = 0; i < str.length(); i++) {
            char c = str.charAt(i);

            if (c == '(' || c == '[') {
                stack.push(c);
                values.push(-1);
            } else {
                if (stack.isEmpty()) {
                    System.out.println(0);
                    return;
                }

                if (c == ')') {
                    if (stack.peek() != '(') {
                        System.out.println(0);
                        return;
                    }
                    stack.pop();

                    int sum = 0;
                    while (!values.isEmpty() && values.peek() != -1) {
                        sum += values.pop();
                    }
                    if (values.isEmpty() || values.peek() != -1) {
                        System.out.println(0);
                        return;
                    }
                    values.pop();
                    values.push(sum == 0 ? 2 : sum * 2);
                } else if (c == ']') {
                    if (stack.peek() != '[') {
                        System.out.println(0);
                        return;
                    }
                    stack.pop();

                    int sum = 0;
                    while (!values.isEmpty() && values.peek() != -1) {
                        sum += values.pop();
                    }
                    if (values.isEmpty() || values.peek() != -1) {
                        System.out.println(0);
                        return;
                    }
                    values.pop();
                    values.push(sum == 0 ? 3 : sum * 3);
                }
            }
        }

        if (!stack.isEmpty()) {
            System.out.println(0);
            return;
        }

        int result = 0;
        while (!values.isEmpty()) {
            if (values.peek() == -1) {
                System.out.println(0);
                return;
            }
            result += values.pop();
        }

        System.out.println(result);
    }
}

```
