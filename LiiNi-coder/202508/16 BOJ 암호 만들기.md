```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.HashSet;
import java.util.List;
import java.util.Set;
import java.util.StringTokenizer;

//TIP 코드를 <b>실행</b>하려면 <shortcut actionId="Run"/>을(를) 누르거나
// 에디터 여백에 있는 <icon src="AllIcons.Actions.Execute"/> 아이콘을 클릭하세요.
public class Main {
    private static BufferedReader br;
    private static int L;
    private static int C;
    private static char[] Arr;
    private static char[] Combination;
    private static StringBuilder answer;
    private static HashSet<Character> mos = new HashSet<>(Set.of('a', 'e', 'i', 'o', 'u'));
    public static void main(String[] args) throws IOException {
       br = new BufferedReader(new InputStreamReader(System.in));
       String[] temp = br.readLine().split(" ");
       L = Integer.parseInt(temp[0]);
       C = Integer.parseInt(temp[1]);
       Arr = new char[C];
       Combination = new char[L];
       StringTokenizer st = new StringTokenizer(br.readLine());
       for(int i = 0; i < C; i++) {
           Arr[i] = st.nextToken().charAt(0);
       }
       Arrays.sort(Arr);
       answer = new StringBuilder();
       dfs(0, 0);
       System.out.println(answer.toString());
       br.close();
   }

    private static void dfs(int startIndex, int depth) {
        if(depth == L){
            if(isFullfill()){
                answer.append(new String(Combination)).append("\n");
            }
            return;
        }
        for(int i = startIndex; i < C; i++){
            Combination[depth] = Arr[i];
            dfs(i + 1, depth + 1);
        }
    }

    private static boolean isFullfill() {
        int countJa = 0;
        int countMo = 0;
        for(char c : Combination){
            if(mos.contains(c)){
                countMo++;
            }else{
                countJa++;
            }
        }
        if(countJa < 2 || countMo < 1){
            return false;
        }
        return true;
    }
}
```
