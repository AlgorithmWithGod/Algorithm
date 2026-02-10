```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder sb = new StringBuilder();
    private static Stack<Character> stack;
    private static char[] input;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(sb.toString() + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        input = br.readLine().toCharArray();
        char[] boom  = br.readLine().toCharArray();
        Stack<Character> temp = new Stack<>();
        stack = new Stack<>();

        for (char c : input) {
            stack.push(c);
            temp.clear();
            int index = boom.length-1;
            while (index >= 0 && !stack.isEmpty() && boom[index] == stack.peek()) {
                temp.push(stack.pop());
                index--;
            }

            if (index != -1) {
                while (!temp.isEmpty()) {
                    stack.push(temp.pop());
                }
            }
        }

        if (stack.isEmpty()) {
            sb.append("FRULA");
        } else {
            while (!stack.isEmpty()) {
                sb.append(stack.pop());
            }
            sb.reverse();
        }
    }
}
```
