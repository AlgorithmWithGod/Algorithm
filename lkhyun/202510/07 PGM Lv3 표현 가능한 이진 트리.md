```java
class Solution {
    public int[] solution(long[] numbers) {
        int[] answer = new int[numbers.length];
        
        for(int i = 0; i < numbers.length; i++){
            answer[i] = isPossible(numbers[i]) ? 1 : 0;
        }
        
        return answer;
    }
    
    public boolean isPossible(long number){
        String binary = Long.toBinaryString(number);
        
        int height = 1;
        while ((1 << height) - 1 < binary.length()) {
            height++;
        }
        int treeSize = (1 << height) - 1;
        
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < treeSize - binary.length(); i++){
            sb.append('0');
        }
        sb.append(binary);
        
        return isValidTree(sb.toString(), 0, treeSize - 1);
    }
    
    private boolean isValidTree(String tree, int start, int end){
        if(start > end) return true;
        
        int mid = (start + end) / 2;
        char root = tree.charAt(mid);
        
        if(root == '0'){
            for(int i = start; i <= end; i++){
                if(tree.charAt(i) == '1') return false;
            }
        }
        
        return isValidTree(tree, start, mid - 1) && 
               isValidTree(tree, mid + 1, end);
    }
}
```
