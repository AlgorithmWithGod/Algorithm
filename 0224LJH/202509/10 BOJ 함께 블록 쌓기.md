```java
import java.io.IOException;
import java.io.*;
import java.util.*;


public class Main {
	static int studentCnt, numCnt,goal;
	static int[][] arr;
	static int[] dp;


   public static void main(String[] args) throws IOException {
      init();
      process();
      print();
   }
   
   public static void init() throws IOException {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      StringTokenizer st = new StringTokenizer(br.readLine());
      studentCnt = Integer.parseInt(st.nextToken());
      numCnt =Integer.parseInt(st.nextToken());
      goal = Integer.parseInt(st.nextToken());
      
      dp = new int[goal+1];
      
      arr = new int[studentCnt][numCnt];
      for (int i = 0; i < studentCnt; i++) {
    	  st = new StringTokenizer(br.readLine());
    	  int idx = 0;
    	  while (st.hasMoreTokens()) {
    		  arr[i][idx++] = Integer.parseInt(st.nextToken());
    	  }
      }

   }

   public static void process() throws IOException {
	   dp[0] = 1;
	   for (int i = 0; i < studentCnt; i++) {
		   int[] temp = new int[goal+1];
		   
		   for (int j = 0 ; j < numCnt; j++) {
			   int num = arr[i][j];
			   if (num == 0) continue;
			   for (int k = 0 ;  k <= goal-num; k++) {
				   temp[k+num] += dp[k];
			   }
			   
		   }
		   
		   for (int j = 0; j <= goal; j++) {
			   dp[j] += temp[j];
			   dp[j] %= 10007;
		   }
	   }
      
   }



   public static void print() {
	   for (int j = 0; j <= goal; j++) {
		   System.out.print(dp[j] + " ");
	   }
	   System.out.println();
	  System.out.println(dp[goal]);
   }
}

```
