```java
class PGM_LV2_전화번호_목록 {

    private static Trie trie;
    private static boolean answer;

    private static class TrieNode {
        TrieNode[] children;
        boolean isEnd;

        TrieNode() {
            children = new TrieNode[10];
            isEnd = false;
        }
    }

    private static class Trie {
        TrieNode root;

        Trie() {
            root = new TrieNode();
        }

        public static boolean insert(String number) {
            TrieNode cur = trie.root;

            int len = number.length();
            for (int i = 0; i < len; i++) {
                int idx = number.charAt(i) - '0';

                if (cur.children[idx] == null) {
                    cur.children[idx] = new TrieNode();
                }

                cur = cur.children[idx];

                if (cur.isEnd) {
                    return false;
                }
            }

            for (int i = 0; i < 10; i++) {
                if (cur.children[i] != null) {
                    return false;
                }
            }
            cur.isEnd = true;
            return true;
        }
    }

    public boolean solution(String[] phone_book) {
        trie = new Trie();

        for (String number : phone_book) {
            if (!trie.insert(number)) {
                return false;
            }
        }
        return true;
    }
}
```
