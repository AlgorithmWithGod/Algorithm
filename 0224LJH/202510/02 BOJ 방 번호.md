```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

class Main {
	// 어차피 숫자간의 순서는 의미 x -> 중요한건 어느 숫자가 몇개있느냐
	// 0만 있는게 아니라면, 숫자의 개수가 많은게 무조건 최고
	
	static int[] cost;
	static int numMax,costMax;
	static ArrayList<ArrayList<Integer>> list = new ArrayList<>();
	
	static StringBuilder sb = new StringBuilder();
	// list.get(i) -> i원을 써서 만들 수 있는 가장 큰 녀석.
	// list.get(i)에 대해서  n개의 숫자를 새로 하는게 cost_0 cost_1 ....cost_n-1이라면 
	// list.get(i) 끝에 0을 붙인거와 list.get(i+ cost_0)과 비교... 이런식으로 진행하면 될듯.

	
    public static void main(String[] args) throws NumberFormatException, IOException {
       init();
       process();
       print();

    }

    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
    	numMax = Integer.parseInt(br.readLine());
    	cost = new int[numMax];
    	
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	for (int i = 0; i < numMax; i++) {
    		cost[i] = Integer.parseInt(st.nextToken());
    	}
    	
    	costMax = Integer.parseInt(br.readLine());
    	for (int i = 0; i<= costMax; i++) {
    		list.add(new ArrayList<>());
    	}

    }
    
    @SuppressWarnings("unchecked")
	public static void process() throws IOException {   
    	for (int i = 0; i < costMax; i++) {
    		
    		for (int j = 0; j < numMax; j++) {
    			if (i + cost[j] > costMax) continue;
    			
    			ArrayList<Integer> temp =  (ArrayList<Integer>) list.get(i).clone();
    			temp.add(j);
    			if (isLarger(temp, list.get(i+cost[j]))) {
    				list.set(i+cost[j], temp);
    			}
    			
    		}
    	}
    	
    	
    	List<Integer> ansList = list.get(costMax);
    	for (int i = 0; i < ansList.size(); i++) {
    		sb.append(ansList.get(i));
    	}
    	if (ansList.isEmpty()) sb.append(0);
    }
    
    private static boolean isLarger(List<Integer> temp, List<Integer> target) {
    	if (temp.get(0) == 0) return false;
    	if (temp.size() > target.size()) return true;
    	else if (temp.size() == target.size()) {
    		for (int i = 0; i < temp.size(); i++) {
    			int tempNum = temp.get(i);
    			int targetNum = target.get(i);
    			
    			if (tempNum > targetNum) return true;
    			else if (tempNum < targetNum) return false;
    		}
    	}
    	
    	return false;
    }
    

   public static void print() {
      System.out.println(sb);
    }
}
```
