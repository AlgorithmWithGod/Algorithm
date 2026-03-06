```java
import java.io.*;
import java.util.*;

public class Main {

    static class Node {
        Map<String, Node> children = new TreeMap<>();
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        Node root = new Node();

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int K = Integer.parseInt(st.nextToken());

            Node current = root;
            for (int j = 0; j < K; j++) {
                String food = st.nextToken();
                current.children.putIfAbsent(food, new Node());
                current = current.children.get(food);
            }
        }

        print(root, 0);
    }

    static void print(Node node, int d) {
        for (String key : node.children.keySet()) {
            for (int i = 0; i < d; i++) {
                System.out.print("--");
            }
            System.out.println(key);

            print(node.children.get(key), d + 1);
        }
    }
}
```
