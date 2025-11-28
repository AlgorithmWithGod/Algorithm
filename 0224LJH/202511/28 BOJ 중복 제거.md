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
	static List<Integer> list = new ArrayList<>();
	static StringBuilder sb = new StringBuilder();
	
    public static void main(String[] args) throws IOException {

        init();
        process();
    	print();

    }
    
    private static void init() throws IOException{
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	while(st.hasMoreTokens()) {
    		list.add(Integer.parseInt(st.nextToken()));
    	}
    	
    }
    
    private static void process() throws IOException {
    	HashSet<Integer> set = new HashSet<>();
    	for (int n: list) {
    		if (set.contains(n)) continue;
    		sb.append(n).append(" ");
    		set.add(n);
    	}
    }
    
	private static void print() {
		System.out.println(sb.toString());
    }

}
```
