```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static Map<Character,Integer> cur;

    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        String str = br.readLine();

        cur = new HashMap<>();

        int max = 0;
        int ans = 0;
        int left = 0, right = 0;

        while(right < str.length()){
            if(cur.size() < N || (cur.size() == N && cur.containsKey(str.charAt(right)))){
               cur.put(str.charAt(right), cur.getOrDefault(str.charAt(right), 0)+1);
               ans++;
               right++;
               max = Math.max(ans,max); 
            }else{
                ans--;
                int temp = cur.get(str.charAt(left));
                if(temp == 1){
                    cur.remove(str.charAt(left++));
                }else{
                    cur.put(str.charAt(left++), temp-1);
                }
            }
        }
        bw.write(max+"");    
        bw.close();
    }
}
```
