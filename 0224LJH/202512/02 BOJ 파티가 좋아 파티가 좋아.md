```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashSet;
import java.util.List;
import java.util.StringTokenizer;

public class Main {
   
   static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
   static StringBuilder sb = new StringBuilder();
   static int partyCnt,day;
   static HashSet<Party> set;
   
   static class Party{
      int start, end,idx;
      
      public Party(int start, int end, int idx) {
    	 this.idx = idx;
         this.start = start;
         this.end = end;
      }
   }
   
    public static void main(String[] args) throws IOException {
       day = 0;
       while(true) {
           partyCnt = Integer.parseInt(br.readLine());
           if (partyCnt == 0 ) break;
           init();
           process();
       }
       print();

    }
    
    private static void init() throws IOException{
       day++;
       set = new HashSet<>();
       for (int i = 0; i < partyCnt; i++) {
          StringTokenizer st = new StringTokenizer(br.readLine());
          int start = Integer.parseInt(st.nextToken());
          int end = Integer.parseInt(st.nextToken());
          set.add(new Party(start, end,i));
       }
    }
    
    private static void process() throws IOException {
       // 23시부터 시작, 제일 늦게 끝나는것부터 찾아서 넣기.
       int cnt = 0;

       for (int i = 23; i >= 8; i--) {

          for (int j = 0; j < 2; j++) {
              int maxDay = 0;
              Party target = null;
              for (Party p: set) {
                  if (p.end > i && p.start <= i ) {
                     if (maxDay < p.start) {
                        maxDay = p.start;
                        target = p;
                     }
                  }
               }
               
               if (target != null) {
                  set.remove(target);
                  cnt++;
               }
          }
       }
       
       String ans  = String.format("On day %d Emma can attend as many as %d parties.\n",day,cnt);
       sb.append(ans);
       
    }
    
   private static void print() {
      System.out.print(sb.toString());
    }

}
```
