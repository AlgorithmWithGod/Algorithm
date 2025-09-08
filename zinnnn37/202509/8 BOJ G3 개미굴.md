```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.Map;
import java.util.StringTokenizer;
import java.util.TreeMap;

public class BJ_14725_개미굴 {

    private static final String edge = "--";

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder sb = new StringBuilder();
    private static StringTokenizer st;

    private static int N;
    private static Trie trie;

    private static class Trie {
        TrieNode root;

        Trie() {
            root = new TrieNode();
        }

        public void insert(String[] words, int length) {
            TrieNode node = root;

            for (int i = 0; i < length; i++) {
                node.children.putIfAbsent(words[i], new TrieNode());
                node = node.children.get(words[i]);
            }
        }

        public void print() {
            for (String food : root.children.keySet()) {
                _print(root.children.get(food), food, 0);
            }
        }

        private void _print(TrieNode cur, String food, int level) {
            for (int i = 0; i < level; i++) {
                sb.append("--");
            }
            sb.append(food).append("\n");

            for (String nextFood : cur.children.keySet()) {
                _print(cur.children.get(nextFood), nextFood, level + 1);
            }
        }
    }

    private static class TrieNode {
        Map<String, TrieNode> children;

        TrieNode() {
            children = new TreeMap<>();
        }
    }

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        trie = new Trie();

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());

            int K = Integer.parseInt(st.nextToken());
            String[] words = new String[K];
            for (int j = 0; j < K; j++) {
                words[j] = st.nextToken();
            }
            trie.insert(words, K);
        }
    }

    private static void sol() throws IOException {
        trie.print();

        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```