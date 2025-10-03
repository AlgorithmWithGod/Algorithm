```java
import java.util.*;

class Solution {
    static int n;
    static int maxWin;
    static int[] answer;
    
    public int[] solution(int[][] dice) {
        n = dice.length;
        maxWin = 0;
        
        combination(new boolean[n], 0, 0, dice);
        
        return answer;
    }
    
    void combination(boolean[] selected, int idx, int count, int[][] dice) {
        if (count == n / 2) {
            int winCount = getWinCount(selected, dice);
            
            if (winCount > maxWin) {
                maxWin = winCount;
                answer = getSelectedDice(selected);
            }
            return;
        }
        
        if (idx == n) return;
        
        selected[idx] = true;
        combination(selected, idx + 1, count + 1, dice);
        
        selected[idx] = false;
        combination(selected, idx + 1, count, dice);
    }
    
    int getWinCount(boolean[] selected, int[][] dice) {
        List<Integer> aList = new ArrayList<>();
        List<Integer> bList = new ArrayList<>();
        
        makeSum(selected, dice, true, 0, 0, aList);
        makeSum(selected, dice, false, 0, 0, bList);
        
        Collections.sort(bList);
        
        int win = 0;
        for (int a : aList) {
            win += lowerBound(bList, a);
        }
        
        return win;
    }
    
    void makeSum(boolean[] selected, int[][] dice, boolean isA, int idx, int sum, List<Integer> list) {
        if (idx == n) {
            list.add(sum);
            return;
        }
        
        if (selected[idx] == isA) {
            for (int num : dice[idx]) {
                makeSum(selected, dice, isA, idx + 1, sum + num, list);
            }
        } else {
            makeSum(selected, dice, isA, idx + 1, sum, list);
        }
    }
    
    int lowerBound(List<Integer> list, int target) {
        int left = 0;
        int right = list.size();
        
        while (left < right) {
            int mid = (left + right) / 2;
            if (list.get(mid) < target) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        
        return left;
    }
    
    int[] getSelectedDice(boolean[] selected) {
        int[] result = new int[n / 2];
        int idx = 0;
        for (int i = 0; i < n; i++) {
            if (selected[i]) {
                result[idx++] = i + 1;
            }
        }
        return result;
    }
}
```
