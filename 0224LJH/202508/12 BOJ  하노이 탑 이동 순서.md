```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;


public class Main {
    static StringBuilder sb = new StringBuilder();
    static int target,cnt;

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        target = Integer.parseInt(br.readLine());
        cnt = 0 ;
    }

    private static void process() throws IOException {
        move (1,3,2,target);
    }

    private static void move(int from, int to, int mid,int size) {
        if ( size ==  1){
            cnt++;
            sb.append(from).append(" ").append(to).append("\n");
            return;
        }

        cnt++;
        move(from, mid , to, size - 1);
        sb.append(from).append(" ").append(to).append("\n");
        move(mid, to , from, size - 1);
    }


    private static void print() {
        System.out.println(cnt);
        System.out.println(sb.toString());
    }
}
```