```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;


public class Main {

    static String[] words;
    static long[] alphabetCnt;
    static long ans;
    static int numCnt;
    static HashSet<Integer> firstLetter  = new HashSet<>();

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        numCnt = Integer.parseInt(br.readLine());
        words = new String[numCnt];
        for (int i = 0; i < numCnt; i++) {
            words[i] = br.readLine();
        }

        alphabetCnt = new long[10];
        ans = 0;
    }

    private static void process() throws IOException {
        for (int i = 0; i < numCnt; i++){
            String t = words[i];
            firstLetter.add(t.charAt(0)-'A');
            for (int j = 0; j < t.length(); j++) {
                alphabetCnt[t.charAt(j)-'A'] += (long) Math.pow(10,t.length() -1 -j);
            }
        }

        long minCnt = Long.MAX_VALUE;
        int minCntAlphabet = -1;
        for (int i = 0; i <= 9; i++){
            if (firstLetter.contains(i))continue;

            if (alphabetCnt[i] < minCnt) {
                minCnt = alphabetCnt[i];
                minCntAlphabet = i;
            }
        }

        alphabetCnt[minCntAlphabet] = 0;

        Arrays.sort(alphabetCnt);

        for (int i = 9; i >= 0; i--){
            ans += alphabetCnt[i] * i;
        }


    }


    private static void print() {
        System.out.println(ans);
    }
}
```