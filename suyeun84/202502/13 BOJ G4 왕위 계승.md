```java
import java.util.*;
import java.io.*;

class Solution
{
	  static ArrayList<Family> famList = new ArrayList<>();
	  static ArrayList<String> candidate = new ArrayList<>();
    static HashMap<String, Double> result = new HashMap<>();
    static double maxNum = 0;
    static String answer = "";
    
	public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        String king = br.readLine().trim();

        result.put(king, 1.0);
        for (int i = 0; i < N; i++) {
        	st = new StringTokenizer(br.readLine());
        	famList.add(new Family(st.nextToken().trim(), st.nextToken().trim(), st.nextToken().trim()));
        }
        for (int i = 0; i < M; i++) {
        	candidate.add(br.readLine().trim());
        }
        
        for (String can : candidate) {
        	double res = dfs(can);
        	if (maxNum < res) {
        		maxNum = res;
        		answer = can;
        	}
        }
        System.out.println(answer);
	}
	
	public static double dfs(String name) {
		if (!result.containsKey(name)) {
			for (Family fam : famList) {
    			if (!fam.c.equals(name)) continue;
            	double res = 0.0;
            	res += (dfs(fam.p1)/2 + dfs(fam.p2)/2);
            	result.put(name, res);
            	break;
            }
    	}
		if (!result.containsKey(name)) result.put(name, 0.0);
		return result.getOrDefault(name, 0.0);
	}
	
	static class Family {
		String c;
		String p1;
		String p2;
		public Family(String c, String p1, String p2) {
			this.c = c;
			this.p1 = p1;
			this.p2 = p2;
		}
	}
}

```
