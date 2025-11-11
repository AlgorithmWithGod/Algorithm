```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.*;
import java.util.*;

public class Main {
	
	static int cnt;
	static PriorityQueue<Integer> pq = new PriorityQueue<>();
			
	public static void main (String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		cnt = Integer.parseInt(br.readLine());
		for (int i = 0; i < cnt; i++) {
			pq.add(Integer.parseInt(br.readLine()));
		}
		
		int goal = 1;
		long hackerCnt = 0;
		
		while(!pq.isEmpty()) {
			if (goal == pq.peek()) {
				goal++;
				pq.poll();
			} else if (goal > pq.peek()) {
				pq.poll();
			} else {
				hackerCnt += pq.peek()-goal;
				pq.poll();
				goal++;
			}
		}
		
		System.out.println(hackerCnt);
		
	}

}

```
