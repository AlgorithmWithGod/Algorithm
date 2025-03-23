```java
import java.io.*;

public class Main {


    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        // 1001 1001001 10010010


        int N = Integer.parseInt(br.readLine());
        StringBuilder sb = new StringBuilder();

        for(int i = 0; i < N; i++) {
            sb.append(br.readLine().matches("(100+1+|01)+")?"YES":"NO").append("\n");
        }
        System.out.println(sb);
    }




    private static int read() throws Exception {
        int d, o;
        d = System.in.read();

        o = d & 15;
        while ((d = System.in.read()) > 32)
            o = (o << 3) + (o << 1) + (d & 15);

        return o;
    }

}


```
