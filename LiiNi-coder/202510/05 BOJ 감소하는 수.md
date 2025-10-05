```java
import java.io.*;
import java.util.*;

public class Main {
    static List<Long> list = new ArrayList<>();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());

        for(int i = 0; i < 10; i++){
            dfs(i, 1);
        }

        Collections.sort(list);
        // for(long l: list){
        //     System.out.print(l + ", ");
        // }
        if(n >= list.size()){
            System.out.println(-1);
        }else{
            System.out.println(list.get(n));
        }
    }

    static void dfs(long num, int depth){
        list.add(num);
        long last = num % 10;
        for(int next = 0; next < last; next++){
            dfs(num * 10 + next, depth + 1);
        }
    }
}

```
