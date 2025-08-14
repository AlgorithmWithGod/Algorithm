```java
import java.io.*;
import java.util.*;

public class Main {
    static int N,K;
    static boolean[] teach = new boolean[26];
    static boolean[] shouldTeach = new boolean[26];
    static int shouldTeachCnt;
    static List<Set<Character>> words = new ArrayList<>();
    static int ans = 0;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        if(K < 5){
            bw.write("0");
            bw.close();
            return;
        }
        K -= 5;
        teach['a' - 'a'] = true;
        teach['c' - 'a'] = true;
        teach['i' - 'a'] = true;
        teach['n' - 'a'] = true;
        teach['t' - 'a'] = true;

        

        for (int i = 0; i < N; i++) {
            String str = br.readLine();
            Set<Character> temp = new HashSet<>();
            for (int j = 4; j < str.length() - 4; j++) {
                shouldTeach[str.charAt(j) - 'a'] = true;
                temp.add(str.charAt(j));
            }
            words.add(temp);
        }

        for (int i = 0; i < shouldTeach.length; i++) {
            if(shouldTeach[i] && !teach[i]) shouldTeachCnt++;
        }

        if(shouldTeachCnt <= K){
            bw.write(N + "");
            bw.close();
            return;
        }
        
        int startPoint = 1;
        while(startPoint < 26 && (!shouldTeach[startPoint] || teach[startPoint])) startPoint++;
        backTracking(startPoint, 0);
        bw.write(ans+"");
        bw.close();
    }
    static void backTracking(int start, int depth){
        if(depth == K){
            ans = Math.max(ans, canReadCount());
            return;
        }

        for (int i = start; i < 26; i++) {
            if(shouldTeach[i] && !teach[i]){
                teach[i] = true;
                backTracking(i+1, depth+1);
                teach[i] = false;
            }
        }
    }
    static int canReadCount(){
        int cnt = 0;
        a: for (Set<Character> s : words) {
            for (Character c : s) {
                if(!teach[c - 'a']){
                    continue a;
                }
            }
            cnt++;
        }
        return cnt;
    }
    
}
```
