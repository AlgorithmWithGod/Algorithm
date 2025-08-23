``` java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

 
public class Main {
	
	static int badLimit,len,ans;
	static boolean[] isBad;
	static char[] word;
	
	static class TrieNode{
		HashMap<Character, TrieNode> map = new HashMap<>();
		
		public void dfs(int badCnt) {
			if (badCnt > badLimit) {
				return;
			}
			ans++;
			
			for (char c: map.keySet()) {
				TrieNode child = map.get(c);
				
				if (isBad[c-'a']) child.dfs(badCnt+1);
				else child.dfs(badCnt);
			}
			
			
		}
	}
	
	static TrieNode root = new TrieNode();

	


	public static void main(String[] args) throws IOException {
		init();
		process();
		print();
	}
   
	public static void init() throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String rawWord = br.readLine();
		len = rawWord.length();
		word = new char[len];
		
		for (int i = 0 ; i < len; i++) {
			word[i] = rawWord.charAt(i);
		}
		
		String[] rawBadGood = br.readLine().split("");
		isBad = new boolean[26];
		for (int i = 0; i < 26; i++) {
			isBad[i] = rawBadGood[i].equals("0");
		}
		
		badLimit = Integer.parseInt(br.readLine());
		ans = -1;
	}
   
	public static void process() {
		for (int i = 0; i < len; i++) {
			insert(i);
		}
		
		root.dfs(0);
		
		
		
	}
	
	public static void insert(int from) {
		TrieNode node =root;
		for (int i = from; i < len; i++) {
			char ch = word[i];
			node = node.map.computeIfAbsent(ch, c -> new TrieNode());
		}
	}
	

   

         

   
	public static void print() {
		System.out.println(ans);
	}
}

```
