```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

//TIP 코드를 <b>실행</b>하려면 <shortcut actionId="Run"/>을(를) 누르거나
// 에디터 여백에 있는 <icon src="AllIcons.Actions.Execute"/> 아이콘을 클릭하세요.
public class Main {
    private static BufferedReader br;
    private static int answer;
    private static int[][] map;
    private static int m;
    private static int n;

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        var temp = br.readLine().split(" ");
        n = Integer.parseInt(temp[0]);
        m = Integer.parseInt(temp[1]);
        map = new int[n][m];
        answer = 0;
        dfs(0);
        System.out.println(answer);
        br.close();
    }

    private static void dfs(int idx) {
        //종료
        if(idx == n*m){
            answer++;
            return;
        }
        //idx에 네모 없는 것으로 진행
        int r = idx / m;
        int c = idx % m;
        map[r][c] = 0;
        dfs(idx+1);

        if(isValid(idx)){
            map[r][c] = 1;
            dfs(idx+1);
        }
    }

    private static boolean isValid(int idx) {
        int r = idx/m;
        int c = idx% m;
        boolean isFirstCol = c == 0;
        if(isFirstCol) return true;
        if(r == 0){
            return true;
        }
        boolean leftDown = (map[r][c-1] == 1);
        boolean leftUp = (map[r-1][c-1] == 1);
        boolean rightUp = (map[r-1][c] == 1);
        if(leftDown && leftUp && rightUp){
            return false;
        }else{
            return true;
        }
    }
}
```
