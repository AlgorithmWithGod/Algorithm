```java
class Solution {
    public int[] solution(int n) {
        int[][] arr = new int[n][];
        for(int i = 0; i<n ;i++){
            arr[i] = new int[i+1];
        }
        int row = 0, col = 0;
        int num = 1;
        int total = n*(n+1)/2;
        int state = 0; // 0:down, 1:right, 2:up
        while(num <= total){
            arr[row][col] = num++;
            if(state == 0){
                if(row+1 == n || arr[row+1][col] != 0){
                    state = 1;
                    col++;    
                }else{
                    row++;   
                }
            }else if(state == 1){
                if(col == row || arr[row][col+1] != 0){
                    state = 2;
                    row--;
                    col--;
                }else{
                    col++;
                }
            }else if(state == 2){
                if(arr[row-1][col-1] != 0){
                    state = 0;
                    row++;
                }else{
                    row--;
                    col--;
                }
            }
        }
        
        int[] answer = new int[total];
        int idx = 0;
        for(int i = 0; i<n; i++){
            for(int j = 0; j<arr[i].length; j++){
                answer[idx++] = arr[i][j];
            }
        }
        return answer;
    }
}
```
