```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.*;
import java.util.*;

public class Main {
	
	
	static char[] arr;
	static int[] dp;
	static int cnt,ans,len;
	
	static final int CHAR_LEN = 'z'-'a'+1;
	static final int MAX = Integer.MAX_VALUE/2;
	static final int X = -1;
	
	static HashSet<Word> words = new HashSet<>();
	
	static class Word{
		//각 알파벳 몇번 사용했는지 카운트
		int[] count = new int[CHAR_LEN];
		char[] content;
		
		public Word(String w) {
			content = w.toCharArray();
			for (int i = 0; i < content.length; i++) {
				count[content[i]-'a']++;
			}
		}
		
		public int getCost(int idx) {
			int end = idx+ content.length;
			if (arr.length < end) {
				return X;
			}
			
			int[] targetCnt = new int[CHAR_LEN];
			for (int i = idx; i < end; i++) {
				targetCnt[arr[i]-'a']++;
			}
			
			for (int i = 0; i< CHAR_LEN; i++) {
				if (targetCnt[i] != count[i]) return X;
			}
			
			int cost = 0;
			
			for (int i = 0; i < content.length; i++) {
				if (arr[i+idx] != content[i])cost++;
			}
			
			
			
			return cost;
		}
		
	}
	
			
	public static void main (String[] args) throws NumberFormatException, IOException {
		init();

		process();
		print();

	}
	
	public static void init() throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		arr = br.readLine().toCharArray();
		cnt = Integer.parseInt(br.readLine());
		ans = MAX;
		len = arr.length;
		dp = new int[len+1];
		
		
		Arrays.fill(dp,MAX);
		dp[0] = 0;
		
		for (int i = 0; i < cnt; i++) {
			String word = br.readLine();
			words.add(new Word(word));
		}
		
	}
	
	public static void process() {
		for (int i = 0; i < len; i++) {
			for (Word w: words) {
				int cost = w.getCost(i);
				if (cost == X) continue;
				
				dp[i+w.content.length] = Math.min(dp[i+w.content.length], dp[i]+cost);
			}
		}
	}
	
	public static void print() {
		System.out.println(dp[len]==MAX?-1:dp[len]);
	}

}

```
