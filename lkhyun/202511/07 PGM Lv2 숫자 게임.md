```java
import java.util.*;

class Solution {
    public int solution(int[] A, int[] B) {
        int answer = 0;
        
        List<Integer> listB = new ArrayList<>();
        for (int num : B) {
            listB.add(num);
        }
        Collections.sort(listB);
        
        for (int cur : A) {
            int idx = binarySearch(listB, cur);
            
            if (idx < listB.size()) {
                answer++;
                listB.remove(idx);
            } else {
                listB.remove(0);
            }
        }
        
        return answer;
    }
    private int binarySearch(List<Integer> list, int target) {
        int left = 0;
        int right = list.size();
        
        while (left < right) {
            int mid = (left + right) / 2;
            
            if (list.get(mid) <= target) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        
        return left;
    }
}
```
