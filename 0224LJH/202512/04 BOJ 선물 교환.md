```java

import java.util.StringTokenizer;
import java.util.*;
import java.io.*;

public class Main {
   
   static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
   static int size;
   static Student[] students;
   static List<Integer> ans = new ArrayList<>();
   static HashSet<Student> set = new HashSet<>();
   
   static StringBuilder sb = new StringBuilder();
  
   
   static class Student implements Comparable<Student>{
	   int presentCnt = 0;
	   int idx;
	   int target1;
	   int target2;
	   
	   public Student (int idx,int t1, int t2) {
		   this.idx = idx;
		   target1 = t1;
		   target2 = t2;
	   }
	   
	   @Override
	   public int compareTo(Student s) {
		   return Integer.compare(this.presentCnt, s.presentCnt);
	   }
   }
   
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();

    }
    
    private static void init() throws IOException{
    	size = Integer.parseInt(br.readLine());
    	students = new Student[size+1];
    	
    	for (int i = 1; i <= size; i++) {
    		StringTokenizer st = new StringTokenizer(br.readLine());
    		int t1 = Integer.parseInt(st.nextToken());
    		int t2 = Integer.parseInt(st.nextToken());
    		students[i] = new Student(i,t1, t2);
    		set.add(students[i]);
    	}
    	
    	for (int i = 1; i <= size; i++) {
    		Student s = students[i];
    		students[s.target1].presentCnt++;
    		students[s.target2].presentCnt++;
    	}
    }
    
    private static void process() throws IOException {
    	PriorityQueue<Student> pq = new PriorityQueue<>();
    	
    	for (int i = 1; i <= size; i++) {
    		pq.add(students[i]);
    	}
    	
    	while(pq.size() > 0 &&  pq.peek().presentCnt < 2) {
    		Student s = pq.poll();
    		if (!set.contains(s)) continue;
    		set.remove(s);
    		students[s.target1].presentCnt--;
    		students[s.target2].presentCnt--;
    		
    		if (students[s.target1].presentCnt < 2) {
    			pq.add(students[s.target1]);
    		}
    		if (students[s.target2].presentCnt < 2) {
    			pq.add(students[s.target2]);
    		}
    	}
    	
    	for (int i = 1; i <= size; i++) {
    		if ( students[i].presentCnt == 2) ans.add(i);
    	}
    	
    	sb.append(ans.size());
    	if (ans.size() == 0) return;
    	sb.append("\n");
    	for (int n: ans) {
    		sb.append(n).append(" ");
    	}
    	
    	
    }
    
   private static void print() {
      System.out.println(sb);
    }

}
```
