```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

//TIP 코드를 <b>실행</b>하려면 <shortcut actionId="Run"/>을(를) 누르거나
// 에디터 여백에 있는 <icon src="AllIcons.Actions.Execute"/> 아이콘을 클릭하세요.
public class Main {
    private static BufferedReader br;
    private static int[] arr;
    private static int s;
    private static int n;

    public static void main(String[] args) throws IOException {
       br = new BufferedReader(new InputStreamReader(System.in));
       String[] temp = br.readLine().split(" ");
       n = Integer.parseInt(temp[0]);
       s = Integer.parseInt(temp[1]);
       arr = new int[n];
       int i = 0;
       for(String token: br.readLine().split(" ")){
           arr[i++] = Integer.parseInt(token);
       }

       int r = 0;
       int l = 0;
       int sum = 0;
       int answer = Integer.MAX_VALUE;
       while(l < arr.length){
           if(r == arr.length){
               sum -= arr[l++];
           }else
               if(sum < s){
                   // 오른쪽에서 하나 추가해서 더해줘야함
                   sum += arr[r++];
               }else{
                   // 왼쪽에서 하나 제거해서 빼줘야함
                   sum -= arr[l++];
               }
           if(sum >= s) answer = Math.min(answer, r - l);
       }
       if(answer == Integer.MAX_VALUE){
           System.out.println(0);
       }else
           System.out.println(answer);
       br.close();
   }
}
```
