```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {

    static HashMap<Character,Integer> boomWord = new HashMap<>();
    static StringBuilder sb = new StringBuilder();
    static Char[] chars;

    static class Char{

        Char pre = null;
        Char post = null;
        char ch;
        boolean isAlive = true;

        public Char(char ch){
            this.ch = ch;
        }

        public boolean checkBoom(int idx){

            if (boomWord.containsKey(ch) && boomWord.get(ch) == idx) {
                if (idx == boomWord.size()-1) return true;
                if (post== null) return false;

                return post.checkBoom(idx+1);
            }
            return false;
        }

        public Char boom(){
            return processBoom(pre,0);
        }
        private Char processBoom(Char pre, int idx){
            if (idx == boomWord.size()){

                if (this.pre != null && pre != null) {
                    this.pre = pre;
                    pre.post = this;
                }

                return this;
            }
            isAlive = false;

            if ( idx == boomWord.size()-1 && this.post == null) {
                if (pre != null )pre.post = null;
                return pre;
            }
            return post.processBoom(pre,idx+1);
        }

        public Char doReposition(){
            // 폭발단어에 포함안되면 굳이 이동 필요 x;
            if (!boomWord.containsKey(ch)) return this;

            int curIdx = boomWord.get(ch);
            return moveToFirst(curIdx);
        }

        private Char moveToFirst(int idx){
            if (idx == 0 || pre == null ) return this;
            if (!boomWord.containsKey(ch) || boomWord.get(ch) != idx) return this;

            return pre.moveToFirst(idx-1);

        }
    }



    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String input =  br.readLine();

        chars = new Char[input.length()];
        chars[0] = new Char(input.charAt(0));
        for (int i = 1; i < chars.length; i++) {
            chars[i] = new Char(input.charAt(i));
            chars[i].pre = chars[i-1];
            chars[i-1].post = chars[i];
        }

        String target = br.readLine();

        for (int i = 0; i < target.length(); i++) {
            boomWord.put(target.charAt(i), i);
        }

    }

    private static void process() {

        Char cur = chars[0];

        while (cur != null) {
            if(cur.checkBoom(0)){
                cur = cur.boom();
                if (cur != null) cur = cur.doReposition();
            } else{
                cur = cur.post;
            }
        }


        for (int i = 0; i < chars.length; i++) {
            if (chars[i].isAlive) sb.append(chars[i].ch);
        }



    }




    private static void print() {
        System.out.println(sb.length()==0 ? "FRULA" : sb.toString());
    }
}
```