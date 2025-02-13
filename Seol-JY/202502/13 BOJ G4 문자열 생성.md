```java
import java.io.*;
import java.util.*;
public class Main {
    private static int count = 0;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw  = new BufferedWriter(new OutputStreamWriter(System.out));
        int N = Integer.parseInt(br.readLine());
    
        String[] arr = new String[N];
        for (int i = 0; i < N; i++) {
            arr[i] = br.readLine();
        }

        int a = 0;
        int b = N - 1;
        while (a <= b) {
            if (arr[a].compareTo(arr[b]) > 0) {
                write(bw, arr[b]);
                b--;
            } else if(arr[a].compareTo(arr[b]) == 0) {
                int innerA = a;
                int innerB = b;
                boolean go = false;
                while (innerA < innerB) {
                    int innerCompare = arr[innerA].compareTo(arr[innerB]);
                    if (innerCompare > 0) {
                        write(bw, arr[b]);
                        b--;
                        go = true;
                        break;
                    } else if (innerCompare < 0) {
                        write(bw, arr[a]);
                        a++;
                        go = true;
                        break;
                    }
                    innerA++;
                    innerB--;
                }
                if (!go) {
                    write(bw, arr[a]);
                    a++;
                }
            } else {
                write(bw, arr[a]);
                a++;
            }
        }

        bw.flush();
        bw.close();
    }

    private static void write(BufferedWriter bw, String target) throws IOException {
        if (count % 80 == 0) {
            if (count!=0) {
                bw.write("\n");
            }
        }
        bw.write(target);
        count++;
    }
}
```
