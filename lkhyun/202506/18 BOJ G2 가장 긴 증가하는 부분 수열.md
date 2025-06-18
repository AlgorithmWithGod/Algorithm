```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static List<Integer> LIS;

    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        LIS = new ArrayList<>();
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            int cur = Integer.parseInt(st.nextToken());
            if(LIS.isEmpty() || LIS.get(LIS.size()-1) < cur){
                LIS.add(cur);
            }else{
                LIS.set(binarySearch(cur),cur);
            }
        }
        bw.write(LIS.size() + "\n");
        bw.close();
    }
    public static int binarySearch(int target) {
        int left = 0; int right = LIS.size() - 1;
        while(left < right){
            int mid = (left + right) / 2;
            if(LIS.get(mid) < target){
                left = mid + 1;
            }else{
                right = mid;
            }
        }
        return left;
    }
}
```
