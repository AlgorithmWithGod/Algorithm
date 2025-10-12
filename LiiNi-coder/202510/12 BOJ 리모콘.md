```java
import java.io.*;
import java.util.*;

public class Main {
    private static boolean[] Broken = new boolean[10];
    private static int Target;
    private static int M;
    private static List<Integer> availableButtons = new ArrayList<>();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        Target = Integer.parseInt(br.readLine());
        M = Integer.parseInt(br.readLine());

        if(M > 0){
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int i = 0; i < M; i++) {
                int b = Integer.parseInt(st.nextToken());
                Broken[b] = true;
            }
        }

        for(int i = 0; i <= 9; i++) {
            if (!Broken[i]) availableButtons.add(i);
        }
        int minPress = Math.abs(Target - 100);
        for(int num = 0; num <= 999999; num++){
            if (canMake(num)) {
                int pressCount = String.valueOf(num).length() + Math.abs(num - Target);
                //System.out.println(pressCount);
                minPress = Math.min(minPress, pressCount);
            }
        }
        System.out.println(minPress);
        br.close();
    }

    private static boolean canMake(int num) {
        if(num == 0)
            return !Broken[0];
        while(num > 0){
            if (Broken[num%10])
                return false;
            num /= 10;
        }
        return true;
    }
}

```
