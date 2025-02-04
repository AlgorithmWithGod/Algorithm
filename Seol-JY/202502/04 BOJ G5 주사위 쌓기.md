```java
import java.util.*;
import java.io.*;

public class Main {
    private static int SIZE;
    private static final int[] crossIndexes = {5, 3 ,4 ,1, 2, 0};
    
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        SIZE = Integer.parseInt(br.readLine());
        Dice[] dices = new Dice[SIZE];
        
        int answer = 0;
        
        StringTokenizer st;
        for (int i = 0; i < SIZE; i++) {
        	st = new StringTokenizer(br.readLine());
        	dices[i] = new Dice(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()),Integer.parseInt(st.nextToken()) ,Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()));
        }
        
        for (int i = 0; i < 6; i++) {
        	int partialMax = dices[0].getSideMaxByIndex(i);
        	int nextTopValue = dices[0].getTopValueByIndex(i);
        	for (int j = 1; j < SIZE; j++) {
        		partialMax += dices[j].getSideMaxByValue(nextTopValue);
        		nextTopValue = dices[j].getTopValueByVlaue(nextTopValue); 
        	}
        	
        	answer = Math.max(partialMax, answer);
        }
        
        System.out.println(answer);
    }
    
    
    public static class Dice {
    	int[] numbers;
    	public Dice(int ...numbers) {
    		this.numbers = numbers;
    	}
    	
    	public int getSideMaxByValue(int bottomValue) {
    		int max = 0;
    		int topValue = getTopValueByVlaue(bottomValue);
    		for (int i = 0; i < 6; i++) {
    			if (numbers[i] == bottomValue || numbers[i] == topValue) continue;
    			max = Math.max(max, numbers[i ]);
    		}
    		return max;
    	}
    	
    	public int getSideMaxByIndex(int bottomIndex) {
    		int max = 0;
    		int topValue = getTopValueByVlaue(numbers[bottomIndex]);
    		for (int i = 0; i < 6; i++) {
    			if (numbers[i] == numbers[bottomIndex] || numbers[i] == topValue) continue;
    			max = Math.max(max, numbers[i]);
    		}
    		return max;
    	}
    	
    	public int getTopValueByVlaue(int bottomValue) {
    		for (int i = 0; i < 6; i++) {
    			if (numbers[i] == bottomValue) {
    				return getTopValueByIndex(i);
    			}
    		}
    		
    		return -1;
    	}
    	
    	public int getTopValueByIndex(int bottomIndex) {
    		return numbers[crossIndexes[bottomIndex]];
    	}
    }
}

```
