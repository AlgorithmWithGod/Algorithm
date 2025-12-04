```java
import java.io.*;
import java.util.Map;
import java.util.TreeMap;

public class BJ_7432_디스크_트리 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder  sb = new StringBuilder();

    private static int      N;
    private static Trie     trie;
    private static String[] words;

    private static class TrieNode {
        boolean               isEnd;
        Map<String, TrieNode> children;

        TrieNode() {
            children = new TreeMap<>();
            isEnd = false;
        }

    }

    private static class Trie {
        TrieNode root;

        Trie() {
            root = new TrieNode();
        }

        public void insert(String[] words) {
            TrieNode cur = root;

            for (String word : words) {
                cur.children.putIfAbsent(word, new TrieNode());
                cur = cur.children.get(word);
            }
            cur.isEnd = true;
        }

        public void print(int depth, TrieNode cur) {
            for (String word : cur.children.keySet()) {
                appendTabs(depth);
                sb.append(word).append("\n");
                print(depth + 1, cur.children.get(word));
            }
        }

        private void appendTabs(int depth) {
            while (depth-- > 0) {
                sb.append(" ");
            }
        }

    }

    public static void main(String[] args) throws IOException {
        sol();
    }

    private static void sol() throws IOException {
        N = Integer.parseInt(br.readLine());
        trie = new Trie();

        while (N-- > 0) {
            words = br.readLine().split("\\\\");
            trie.insert(words);
        }
        trie.print(0, trie.root);
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```