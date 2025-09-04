```java
import java.io.IOException;
import java.io.*;
import java.util.*;


public class Main {
   static int villageCnt, totalSpace, curSpace,ans, deliveryCnt;
   static PriorityQueue<Delivery> pq = new PriorityQueue<>();
   static int[] spaces;
   static Delivery[] deliveries;

   
   static class Delivery implements Comparable<Delivery>{
      int from;
      int to;
      int boxCnt;
      int overlap = 0;
      
      public Delivery(int from, int to, int boxCnt) {
         this.from = from;
         this.to = to;
         this.boxCnt = boxCnt;
      }
      
      @Override
      public int compareTo(Delivery d) {
    	  
         return Integer.compare(this.to,d.to);
      }
   }

   public static void main(String[] args) throws IOException {
      init();
      process();
      print();
   }
   
   public static void init() throws IOException {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      StringTokenizer st = new StringTokenizer(br.readLine());
      villageCnt = Integer.parseInt(st.nextToken());
      totalSpace =Integer.parseInt(st.nextToken());
      curSpace = 0;
      ans = 0;
      
      spaces = new int[villageCnt+1];
      deliveryCnt = Integer.parseInt(br.readLine());
      deliveries = new Delivery[deliveryCnt];
     
      for (int i = 0; i < deliveryCnt; i++) {
         st = new StringTokenizer(br.readLine());
         int from = Integer.parseInt(st.nextToken());
         int to = Integer.parseInt(st.nextToken());
         int boxCnt = Integer.parseInt(st.nextToken());
         
         Delivery d = new Delivery(from,to,boxCnt);
         deliveries[i] = d;
         
      }
      
      
      
   }

   public static void process() throws IOException {
	   getOverlap();
	   for (int i = 0; i < deliveryCnt; i++) pq.add(deliveries[i]);

      while(!pq.isEmpty()) {
         Delivery d = pq.poll();
         
         put(d);
      }
      
      
   }
   
   public static void put(Delivery d) {
      
      int limit = d.boxCnt;
            
      for (int i = d.from; i < d.to; i++) {
         limit = Math.min(limit, totalSpace - spaces[i]);
      }
      
      for (int i = d.from; i <d.to; i++) {
    	  spaces[i] += limit;
      }
      ans += limit;
   }
   
   public static void getOverlap() {
	   int[] cumul = new int[villageCnt+1];
	   
	   for (int i = 0; i < deliveryCnt; i++) {
		   Delivery d = deliveries[i];
		   for (int j = d.from; j < d.to; j++) {
			   cumul[j]++;
		   }
	   }
	   
	   for (int i = 0; i < deliveryCnt; i++) {
		   Delivery d = deliveries[i];
		   int maxCnt = 0;
		   for (int j = d.from; j < d.to; j++) {
			   maxCnt = Math.max(maxCnt, cumul[j]);
		   }
		   d.overlap = maxCnt;
	   }
   }
   


   


   public static void print() {
	   for (int i =1 ; i <= villageCnt; i++) System.out.print(spaces[i] + " ");
	   System.out.println();
      System.out.println(ans);
   }
}

```
