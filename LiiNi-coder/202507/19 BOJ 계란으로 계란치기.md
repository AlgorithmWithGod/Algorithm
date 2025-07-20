```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    private static BufferedReader br;
    private static int n;
    private static int[] ws;
    private static int[] ss;
    private static int answer;

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        ss = new int[n];
        ws = new int[n];
        for (int i = 0; i < n; i++) {
            String[] temp = br.readLine().split(" ");
            ss[i] = Integer.parseInt(temp[0]);
            ws[i] = Integer.parseInt(temp[1]);
        }
        answer = 0;
        dfs(0);
        System.out.println(answer);
        br.close();
    }

    private static void dfs(int now) {
        if(now == n){
            // 완탐 리프 - 깨진 계란 개수 세기
            int count = 0;
            for (int i = 0; i < n; i++) {
                if(ss[i] <= 0) count++;
            }
            answer = Math.max(answer, count); // 반복문 밖으로 이동
            return;
        }
        
        // 현재 계란이 이미 깨져있으면 바로 다음으로
        if(ss[now] <= 0) {
            dfs(now + 1);
            return;
        }
        
        boolean canHit = false;
        
        for(int target = 0; target < n; target++) {
            if(now == target || ss[target] <= 0) continue;
            
            canHit = true;
            
            // 서로 치기
            ss[now] -= ws[target];
            ss[target] -= ws[now];
            
            dfs(now + 1);
            
            // 상태 복구
            ss[now] += ws[target];
            ss[target] += ws[now];
        }
        
        if(!canHit) {
            dfs(now + 1);
        }
    }
}
```
