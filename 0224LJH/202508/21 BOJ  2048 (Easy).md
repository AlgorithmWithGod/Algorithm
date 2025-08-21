```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;


public class Main {
   
   static final int END = 5;
   static final int UP = 0;
   static final int RIGHT = 1;
   static final int DOWN = 2;
   static final int LEFT = 3;
   
   static int[][] arr;
   static int[] dy = {-1,0,1,0};
   static int[] dx = {0,1,0,-1};
   static int size,ans;
   
   

   public static void main(String[] args) throws IOException {
      init();
      process();
      print();
   }
   
   public static void init() throws IOException {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      size = Integer.parseInt(br.readLine());
      arr = new int[size][size];
      ans = 0;
      
      for (int i = 0; i < size; i++) {
         StringTokenizer st = new StringTokenizer(br.readLine());
         for (int j = 0; j < size; j++) {
            arr[i][j] = Integer.parseInt(st.nextToken());
         }
      }

      
   }
   
   public static void process() {
	   dfs(arr, 0);
   }
   
   public static void dfs(int[][] board, int cnt) {
      if (cnt == END) {
         for (int i = 0 ; i < size; i++) {
            for (int j = 0; j < size; j++) {
            	System.out.print(board[i][j]+ " ");
            	ans = Math.max(board[i][j],ans);
            }
            System.out.println();
         }
         System.out.println();
         return;
      }
      
      
      //dir으로 이동하면 dir부터 큐에 넣은 후, 하나씩 꺼내면 됨. 이걸 유지
      
      for (int dir = 0 ; dir < 4; dir++) {
         Queue<Integer>[] qs = new Queue[size];
         int[][] temp = new int[size][size];
         boolean keepTrying = false;
         
         
         for (int i = 0 ; i < size; i++) {
            qs[i] = new LinkedList<Integer>(); 
            for (int j = 0; j < size; j++) {
               int num = 0;
               
               if (dir == UP) num = board[j][i]; // 위에서부터 아래 순으로 담김
               else if (dir == DOWN) num = board[size-1-j][i]; // 아래에서부터 위로
               else if (dir == LEFT) num = board[i][j];
               else if (dir == RIGHT) num = board[i][size-1-j];
               
               if (num != 0 ) qs[i].add(num);
            }
         }
         
         for (int i = 0 ; i < size; i++) {
            Queue q = qs[i];
            int idx = 0;
            
            while (!q.isEmpty()) {
               int target = -1; // 지금 보고있는 칸.
               
               if (dir == UP) target = temp[idx][i]; // 위에서부터 아래 순으로 담김
               else if (dir == DOWN) target = temp[size-1-idx][i]; // 아래에서부터 위로
               else if (dir == LEFT) target = temp[i][idx];
               else if (dir == RIGHT) target = temp[i][size-1-idx];
               
               
               int num = (int) q.poll();
               
               
               
               if (target != 0 && target != num) idx++;
               
               if (target == num) keepTrying = true;

               if (dir == UP) temp[idx][i] += num;
               else if (dir == DOWN) temp[size-1-idx][i] += num;
               else if (dir == LEFT) temp[i][idx] += num;
               else if (dir == RIGHT) temp[i][size-1-idx] += num;
                  
               if (target == num) idx++; // 합쳐진것. 이제 이 칸에 볼일없음               
               
            }
            
            
            
            
         }
         
         dfs(temp,cnt+1);
         
      }
      
   }
   

   

   public static void print() {
      System.out.println(ans);
   }
}

```
