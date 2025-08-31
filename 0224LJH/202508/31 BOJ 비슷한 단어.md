```java
import java.io.*;
import java.util.*;

public class Main {

    static int size,ansIdx, longest=0;
    static String ans1,ans2;
    static String[] words;

    static class TrieNode{
        Map<Character, TrieNode> children = new HashMap<>();
        String word;
        int num;
        boolean isWord;

        public TrieNode(String word, int num){
            this.word = word;
            this.num = num;
        }
    }

    static void insert(String nWord, int wordNum){
        TrieNode node = root;
        int len = 0;
        int tempIdx = 0;
        boolean isEnd = false;
        String tempWord = "";

        for (int i = 0; i < nWord.length(); i++){
            Character c = nWord.charAt(i);
            if (node.children.containsKey(c)){
                node = node.children.get(c);
                if (!isEnd){
                    len++;
                    tempWord = node.word;
                    tempIdx = node.num;
                }
            } else {
                node.children.put(c, new TrieNode(nWord,wordNum));
                node = node.children.get(c);
                isEnd = true;
            }
        }

        if (longest < len || (longest == len && tempIdx < ansIdx )){
            ansIdx = tempIdx;
            longest = len;
            ans1 = tempWord;
            ans2 = nWord;
        }
    }

    static TrieNode root = new TrieNode("",-1);

    public static void main(String[] args) throws Exception {
        init();
        process();
        print();

    }

    public static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        size =Integer.parseInt(br.readLine());
        words = new String[size];
        ansIdx = -1;
        for (int i = 0; i < size; i++) {
            words[i] = br.readLine();

        }
    }

    public static void process(){
        for(int i = 0; i < size; i++){
            insert(words[i],i);
//            System.out.println("longest = " + longest);
//            System.out.println("ans1 = " + ans1);
//            System.out.println("ans2 = " + ans2);
        }
    }

    public static void print(){
        System.out.println(longest);
        System.out.println(ans1);
        System.out.println(ans2);
    }


}
```
