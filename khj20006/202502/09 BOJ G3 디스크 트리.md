```java

import java.util.*;
import java.io.*;

class Node{
    String name;
    TreeMap<String, Node> subs;
    Node(String name){
        this.name = name;
        subs = new TreeMap<String, Node>();
    }
}

class Trie{
    Node root;
    Trie(){
        root = new Node("ROOT");
    }
}

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static long nextLong() {return Long.parseLong(st.nextToken());}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	static Trie trie;
	static int N;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
		
		bwEnd();
	}
	
	static void ready() throws Exception{
    
        N = Integer.parseInt(br.readLine());
        trie = new Trie();

	}
	
	static void solve() throws Exception{
		
		while(N-- > 0){
		    String line = br.readLine();
		    String[] dirs = line.split("\\\\");
		    Node cur = trie.root;
		    for(String dir : dirs){
		        if(!cur.subs.containsKey(dir)) cur.subs.put(dir, new Node(dir));
		        cur = cur.subs.get(dir);
		    }
		    
		}
		
		print(trie.root, -1);
		
	}
	
	static void print(Node cur, int dep) throws Exception{
	    if(dep >= 0){
    	    for(int i=0;i<dep;i++) bw.write(" ");
    	    bw.write(cur.name + "\n");
	    }
	    for(String key : cur.subs.keySet()){
	        Node val = cur.subs.get(key);
	        print(val, dep+1);
	    }
	}
	
}

```
