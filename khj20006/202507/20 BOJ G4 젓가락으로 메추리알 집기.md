```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    public static void main(String[] args) throws Exception {
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        for(int i=1;i<=N;i++) for(int j=(i%2==1 ? 2 : 1);j<=M;j+=2) {
            bw.write("? " + i + " " + j + "\n");
            bw.flush();
            if(br.readLine().equals("1")) return;
        }

    }

}
```
