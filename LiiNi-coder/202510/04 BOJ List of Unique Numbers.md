```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(                                                                                                                                                             new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        int[] arr = new int[N];
        for(int i = 0; i < N; i++){
            arr[i] = Integer.parseInt(st.nextToken());
        }

        long result = 0;
        int l = 0;
        int MAX = 100000;

        int[] freq = new int[MAX + 1];
        for(int r = 0; r < N; r++){
            freq[arr[r]]++;
            while(freq[arr[r]] > 1){
                freq[arr[l]]--;
                l++;
            }
            result += (r - l +1);
        }

        System.out.println(result);
    }
}

```
