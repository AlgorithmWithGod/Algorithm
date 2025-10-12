```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringBuilder sb = new StringBuilder();
    static int G;

    public static void main(String[] args) throws Exception {
        G = Integer.parseInt(br.readLine());
        List<Integer> results = new ArrayList<>();
        for (int b = 1; b * b <= G; b++) {
            if (G % b == 0) {
                int a = G / b;
                
                if ((a + b) % 2 == 0) {
                    int c = (a + b) / 2;
                    int p = (a - b) / 2;
                    
                    if (p >= 1) {
                        results.add(c);
                    }
                }
            }
        }
        
        if (results.isEmpty()) {
            bw.write("-1");
        } else {
            Collections.sort(results);
            for (int weight : results) {
                bw.write(weight + "\n");
            }
        }
        
        bw.close();
    }
}
```
