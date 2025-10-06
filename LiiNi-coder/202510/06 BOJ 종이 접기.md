```java
import java.io.*;
import java.util.*;

public class Main{
    static boolean check(String s){
        if(s.length() == 1)
            return true;
        int mid=s.length() / 2;
        for(int i=0; i < mid; i++){
            if(s.charAt(i) == s.charAt(s.length()- 1 - i))
                return false;
        }
        return check(s.substring(0, mid)) && check(s.substring(mid+ 1));
    }

    public static void main(String[] args)throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(br.readLine());
        StringBuilder sb=new StringBuilder();
        while(t-->0){
            sb.append(check(br.readLine() ) ? "YES\n" : "NO\n");
        }

        System.out.print(sb.toString());
        br.close();
    }
}

```
