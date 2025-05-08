```java

import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int[] p;

    public static void main(String[] args) throws IOException{
        char[] str = br.readLine().toCharArray();
        char[] pattern = br.readLine().toCharArray();
        p = new int[pattern.length];

        for (int i = 1,j = 0; i < pattern.length; i++) {
            while(j>0 && pattern[i] != pattern[j]){
                j = p[j-1];
            }
            if(pattern[i] == pattern[j]){
                p[i] = ++j;
            }
        }
        char[] res = new char[str.length];
        int[] len = new int[str.length];
        int ptr = 0;
        for (int i = 0,j; i < str.length; i++) {
            res[ptr] = str[i];
            j = (ptr == 0) ? 0 : len[ptr-1];
            while(j>0 && str[i] != pattern[j]){
                j = p[j-1];
            }
            if(str[i] == pattern[j]) {
                j++;
            }
            len[ptr] = j;
            ptr++;

            if(j == pattern.length){
                ptr -= j;
            }
        }
        if(ptr == 0){
            bw.write("FRULA");
        }else{
            bw.write(new String(res,0,ptr));
        }
        bw.close();
    }
}
```
