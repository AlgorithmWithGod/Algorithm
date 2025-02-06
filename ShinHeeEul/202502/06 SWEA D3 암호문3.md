```java
import java.util.*;
 
import javax.xml.parsers.*;
 
import org.xml.sax.helpers.DefaultHandler;
 
import java.io.*;
 
public class Solution {
 
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
 
        StringBuilder sb = new StringBuilder();
        for(int t = 1; t <= 10; t++) {
        int N = Integer.parseInt(br.readLine());
         
        ArrayList<Integer> list = new ArrayList<>();
        StringTokenizer st = new StringTokenizer(br.readLine());
         
        for(int i = 0; i < N; i++) {
             
            list.add(Integer.parseInt(st.nextToken()));
        }
         
        int M = Integer.parseInt(br.readLine());
 
        st = new StringTokenizer(br.readLine());
        for(int i = 0; i < M; i++) {
             
            char c = st.nextToken().charAt(0);
             
            if(c == 'I') {
                int x = Integer.parseInt(st.nextToken());
                int y = Integer.parseInt(st.nextToken());
                 
                ArrayList<Integer> lis = new ArrayList<>();
                 
                for(int j = 0; j < y; j++) lis.add(Integer.parseInt(st.nextToken()));
                 
                for(int j = lis.size() - 1; j >= 0; j--) {
                    list.add(x, lis.get(j));
                }
                 
            } else if(c == 'D') {
                int x = Integer.parseInt(st.nextToken());
                int y = Integer.parseInt(st.nextToken());
                while(y --> 0)
                    list.remove(x);
            } else {
                int y = Integer.parseInt(st.nextToken());
                ArrayList<Integer> lis = new ArrayList<>();
                 
                for(int j = 0; j < y; j++) lis.add(Integer.parseInt(st.nextToken()));
                 
                list.addAll(lis);
            }
        }
        sb.append("#").append(t).append(" ");
         
        for(int i = 0; i < 10; i++) sb.append(list.get(i)).append(" ");
         
        sb.append("\n");
         
        }
         
        System.out.println(sb);
    }
 
}
```
